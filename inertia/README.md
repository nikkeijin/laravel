# Server Side

> Dependencies

Install the Inertia server-side adapter
```
composer require inertiajs/inertia-laravel
```

> View

resource/view/app.blade.php
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    @vite('resources/js/app.js')
    @inertiaHead
  </head>
  <body>
    @inertia
  </body>
</html>
```

This template should include your assets, as well as the @inertia and @inertiaHead directives.

> Middleware

```
sail artisan inertia:middleware
```

Once the middleware has been published, register the HandleInertiaRequests middleware in your App\Http\Kernel as the LAST ITEM in your web middleware group.

```
'web' => [
    \App\Http\Middleware\HandleInertiaRequests::class,
],
```

# Client Side

> Dependencies

Install the Inertia client-side adapter:
```
npm install @inertiajs/vue3
```

> Vue 3

```
npm install vue@next
```

> Initialize the Inertia app

resource/js/app.js
```
import { createApp, h } from 'vue'
import { createInertiaApp } from '@inertiajs/vue3'

createInertiaApp({
  resolve: name => {
    const pages = import.meta.glob('./Pages/**/*.vue', { eager: true })
    return pages[`./Pages/${name}.vue`]
  },
  setup({ el, App, props, plugin }) {
    createApp({ render: () => h(App, props) })
      .use(plugin)
      .mount(el)
  },
})
```

> Vite

```
npm i @vitejs/plugin-vue
```

vite.config.js
```
import { defineConfig } from "vite";
import laravel from "laravel-vite-plugin";
import vue from "@vitejs/plugin-vue";

export default defineConfig({
  plugins: [
    laravel({
      input: ["resources/css/app.css", "resources/js/app.js"],
      refresh: true,
    }),
    vue({
      template: {
        transformAssetUrls: {
          base: null,
          includeAbsolute: false,
        },
      },
    }),
  ],
});
```

# Install our dependencies and compile our files
```
npm install
npm run dev
```

# Pages

Create Pages folder inside resources/js/

Example    
resources/js/Pages/Index.vue   

The route for    

routes/web.php
```
use Inertia\Inertia;

Route::get('/', function () {
    return Inertia::render('Index');
});
```

> An example of Route via controller

route/web.php
```
use App\Http\Controllers\SampleController;

Route::get('/sample',[SampleController::class, 'sample']);
```

Create the controller for
```
sail artisan make:controller SampleController
```

app/Http/Controllers/SampleController.php
```
namespace App\Http\Controllers;

use Illuminate\Http\Request;

use Inertia\Inertia;

class SampleController extends Controller
{
    public function sample()
    {
        return Inertia::render('Sample');
    }
}
```
