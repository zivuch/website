---
title: File Uploads and Validation
menu_order: 13
post_status: publish
post_excerpt: Learn how to upload files in NestJS using Multer, and combine file handling with DTO validation for secure and structured input.
taxonomy:
  category:
    - nestjs
    - Practical Guide to NestJS
  post_tag:
    - nestjs
    - multer
    - file-upload
    - validation
    - dto
    - multipart
---

<div class="toc" markdown="1">

## On this Page

- [Setting Up Multer in NestJS](#setting-up-multer-in-nestjs)
- [Uploading a Single File](#uploading-a-single-file)
- [Handling File + DTO Validation](#handling-file--dto-validation)
- [Validating File Type and Size](#validating-file-type-and-size)
- [Storing Files on Disk or in Memory](#storing-files-on-disk-or-in-memory)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Setting Up Multer in NestJS

NestJS integrates with **Multer**, a popular middleware for handling `multipart/form-data`.

It's already included via `@nestjs/platform-express`.

No installation needed!

---

## Uploading a Single File

In your controller:

```ts
import { Controller, Post, UploadedFile, UseInterceptors } from '@nestjs/common';
import { FileInterceptor } from '@nestjs/platform-express';

@Controller('upload')
export class UploadController {
  @Post()
  @UseInterceptors(FileInterceptor('file'))
  upload(@UploadedFile() file: Express.Multer.File) {
    return {
      originalName: file.originalname,
      size: file.size,
    };
  }
}
```

Use `POST /upload` with a `form-data` body and a key called `file`.

---

## Handling File + DTO Validation

You can upload a file and JSON body at the same time:

```ts
@Post()
@UseInterceptors(FileInterceptor('cover'))
upload(
  @UploadedFile() cover: Express.Multer.File,
  @Body() postDto: CreatePostDto,
) {
  return { ...postDto, cover: cover.originalname };
}
```

DTO:

```ts
export class CreatePostDto {
  @IsString()
  title: string;

  @IsString()
  content: string;
}
```

The JSON data and the file are processed together.

---

## Validating File Type and Size

Custom logic for file validation:

```ts
upload(
  @UploadedFile() file: Express.Multer.File,
) {
  if (!file.mimetype.startsWith('image/')) {
    throw new BadRequestException('Only image files allowed');
  }
  if (file.size > 5 * 1024 * 1024) {
    throw new BadRequestException('File too large');
  }
  return file;
}
```

You can also use Multer options to filter files:

```ts
@UseInterceptors(FileInterceptor('file', {
  fileFilter: (req, file, cb) => {
    file.mimetype.startsWith('image/')
      ? cb(null, true)
      : cb(new Error('Only images allowed'), false);
  },
}))
```

---

## Storing Files on Disk or in Memory

By default, files are stored in memory (buffered).

To save on disk:

```ts
@UseInterceptors(FileInterceptor('file', {
  storage: diskStorage({
    destination: './uploads',
    filename: (req, file, cb) => {
      const name = `${Date.now()}-${file.originalname}`;
      cb(null, name);
    },
  }),
}))
```

Don’t forget to make the `/uploads` folder accessible if needed.

---

## Summary

- Use `FileInterceptor` from `@nestjs/platform-express` to handle file uploads
- Combine `@UploadedFile()` and `@Body()` to validate file + form data together
- Validate file type and size manually or with Multer options
- Save files in memory (default) or configure disk storage

> Next: **Lesson 14 – NestJS + Swagger for API Docs**

</div>
