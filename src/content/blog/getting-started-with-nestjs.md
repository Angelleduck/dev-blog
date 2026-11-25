---
title: "Getting Started with NestJS"
description: "A quick look at the pieces that make up a small NestJS API."
category: "Backend"
pubDate: 2026-11-20
cover: "../../assets/Nestjs.png"
coverAlt: "NestJS logo and name next to a black cat"
---

NestJS is a framework for building server-side applications with Node.js. It supports TypeScript out of the box and gives an app a clear structure. That structure can be helpful when a project grows beyond one or two routes.

An API is a good place to start: the browser sends a request, and the server sends back data. In NestJS, that work is usually split between a module, a controller, and a service.

## The main pieces

- A **module** groups related parts of the app. A notes feature, for example, can have its own `NotesModule`.
- A **controller** handles incoming requests. It connects a URL such as `/notes` to a method.
- A **service** contains the logic or data the controller needs. Keeping it separate makes the controller easier to read.

NestJS uses *dependency injection* to give a controller access to its service. Instead of creating the service inside every route, the controller receives it through its constructor.

## A small notes API

The following example keeps the notes in memory, so they will disappear when the server restarts. That is enough to see how the three pieces work together:

```ts
import { Controller, Get, Injectable, Module } from "@nestjs/common";

@Injectable()
class NotesService {
  private readonly notes = ["Learn NestJS", "Build an API"];

  findAll() {
    return this.notes;
  }
}

@Controller("notes")
class NotesController {
  constructor(private readonly notesService: NotesService) {}

  @Get()
  findAll() {
    return this.notesService.findAll();
  }
}

@Module({
  controllers: [NotesController],
  providers: [NotesService],
})
export class NotesModule {}
```

After importing `NotesModule` into the application's root module, a `GET /notes` request reaches the controller. The controller calls the service, which returns the list. NestJS then sends that list as a JSON response.

The decorators have different jobs: `@Controller("notes")` sets the base path, `@Get()` handles a GET request, and `@Injectable()` marks the service for dependency injection.

## Where to go from here

The next step could be a `GET /notes/:id` route that returns one note, followed by a route that adds a note. Those features introduce route parameters and request bodies without changing the basic pattern: the controller handles HTTP, while the service handles the work.

For a real application, the service would usually get its notes from a database rather than an array. Starting with an array makes it easier to understand the route first.
