---
title: Context Project
description: The project object is a proxy in the framework store part of your context and gives you information about the app manifest and some metatags
---

The `project` object is a proxy in the framework store part of your context and gives you information about the app manifest and some metatags.

This key is **readwrite* in the **server* context.

This key is **readonly** in the **client** context.

`project` keys will be used to generate metatags during server-side rendering and must be assigned before [`initiate`](/full-stack-lifecycle) is resolved.

`project` keys will be used to generate the app **manifest** and should be set during the [application startup](/application-startup).

The `disallow` key will be used to generate the **robots.txt** and should be set during the [application startup](/application-startup).

`project` keys are frozen after the [application startup](/application-startup).

The following keys are available in the object:

- **domain**: `string`
- **name**: `string`
- **shortName**: `string`
- **color**: `string`
- **backgroundColor**: `string`
- **type**: `string`
- **display**: `string`
- **orientation**: `string`
- **scope**: `string`
- **root**: `string`
- **icons**: `object`
- **favicon**: `string` (relative or absolute url)
- **disallow**: `string array` (relative paths)
- **sitemap**: `boolean` or `string` (relative or absolute url)
- **cdn**: `string` (absolute url)
- **protocol**: `string` (http or https)

Besides `domain`, `name` and `color` all other keys have sensible defaults generated based on the application scope.

If you do not declare the `icons` key, Nullstack will scan any icons with the name following the pattern "icon-[WIDTH]x[HEIGHT].png" in your public folder.

If the `sitemap` key is set to true your **robots.txt** file will point the sitemap to `https://${project.domain}/sitemap.xml`.

The `cdn` key will prefix your asset bundles and will be available in the context so you can manually prefix other assets.

The `protocol` key is "http" in development mode and "https" in production mode by default

```jsx
import Nullstack from 'nullstack';

class Application extends Nullstack {

  static async start({project}) {
    project.name = 'Nullstack';
    project.shortName = 'Nullstack';
    project.domain = 'nullstack.app';
    project.color = '#d22365';
    project.backgroundColor = '#d22365';
    project.type = 'website';
    project.display = 'standalone';
    project.orientation = 'portrait';
    project.scope = '/';
    project.root = '/';
    project.icons = {
      '72': '/icon-72x72.png',
      '128': '/icon-128x128.png',
      '512': '/icon-512x512.png'
    };
    project.favicon = '/favicon.png';
    project.disallow = ['/admin'];
    project.sitemap = true;
    project.cdn = 'cdn.nullstack.app';
    project.protocol = 'https';
  }

  prepare({project, page}) {
    page.title = project.name;
  }

}

export default Application;
```

> 💡 You can override the automatically generated **manifest.json** and **robots.txt** by serving your own file from the **public** folder

## Next step

⚔ Learn about the [context `settings`](/context-settings).