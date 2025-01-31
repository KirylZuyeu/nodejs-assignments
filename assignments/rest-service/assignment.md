# Assignment: REST Service

## Description

Let's try to create a Home Library Service! `Users` can create, read, update, delete data about `Artists`, `Tracks` and `Albums`, add them to `Favorites` in their own Home Library!

NB! You must create new repository from [template](https://github.com/rolling-scopes-school/nodejs-course-template/generate) for this task. Its name must be nodejs2022Q2-service i.e. full link to the repository must be https://github.com/%your-gihub-id%/nodejs2022Q2-service.

**Create an application, the application should operate with the following resources:**

- `User` (with attributes):
  ```typescript
  interface User {  
    id: string; // uuid v4
    login: string;
    password: string;
    version: number; // integer number, increments on update
    createdAt: number; // timestamp of creation
    updatedAt: number; // timestamp of last update
  }
  ```

- `Artist` (with attributes):
  ```typescript
  interface Artist { 
    id: string; // uuid v4
    name: string;
    grammy: boolean;
  }
  ```
  
- `Track` (with attributes):
  ```typescript
  interface Track { 
    id: string; // uuid v4
    name: string;
    artistId: string; // refers to Artist
    albumId: string | null; // refers to Album
    duration: number; // integer number
  }
  ```

- `Album` (with attributes):
  ```typescript
  interface Album { 
    id: string; // uuid v4
    name: string;
    year: number;
    artistId: string; // refers to Artist
  }
  ```

- `Favorites` (with attributes):
  ```typescript
  interface Favorites {
    artists: string[]; // favorite artists ids
    albums: string[]; // favorite albums ids
    tracks: string[]; // favorite tracks ids
  }
  ```

**Details:**

1. For `Users`, `Artists`, `Albums`, `Tracks` and `Favorites` REST endpoints with separate router paths should be created
  * `Users` (`/user` route)
    * `GET /user` - get all users
    * `GET /user/:id` - get single user by id
    * `POST /user` - create user (following DTO should be used)
    `CreateUserDto`
    ```typescript
        interface CreateUserDto {  
          login: string; 
          password: string;
        }
    ```
    * `PUT /user/:id` - update user's password  
    `UpdatePasswordDto` (with attributes): 
    ```typescript
    interface UpdatePasswordDto {  
      oldPassowrd: string; // previous password
      newPassword: string; // new password
    }
    ```
    * `DELETE /user/:id` - delete user
  
  * `Tracks` (`/track` route)
    * `GET /track` - get all tracks
    * `GET /track/:id` - get single track by id
    * `POST /track` - create new track
    * `PUT /track/:id` - update track info
    * `DELETE /track/:id` - delete track

  * `Albums` (`/album` route)
    * `GET /album` - get all albums
    * `GET /album/:id` - get single album by id
    * `POST /album` - create new album
    * `PUT /album/:id` - update album info
    * `DELETE /album/:id` - delete album

  * `Favorites`
    * `GET /favs` - get all favorites
    * `POST /favs/track/:id` - add track to the favorites
    * `DELETE /favs/track/:id` - delete track from favorites
    * `POST /favs/album/:id` - add album to the favorites
    * `DELETE /favs/album/:id` - delete album from favorites
    * `POST /favs/artist/:id` - add artist to the favorites
    * `DELETE /favs/artist/:id` - delete artist from favorites

2. For now, these endpoints should operate only with **in-memory** (hardcoded) data, in the next tasks we will use a DB for it. You should organize your modules with the consideration that the data source will be changed soon.

3. An `application/json` format should be used for request and response body.

4. Do not put everything in one file - use a separate file for application creation (bootstrapping), for controllers (routers) and code related to business logic. Also split files to different modules depends on a domain (user-related, board-related, etc...).

5. To run the service `npm start` command should be used.

6. Service should listen on PORT `4000`.

**Hints**

* To generate all entities `id`s use [uuid](https://www.npmjs.com/package/uuid) package or [Node.js analogue](https://nodejs.org/dist/latest-v16.x/docs/api/crypto.html#cryptorandomuuidoptions).
