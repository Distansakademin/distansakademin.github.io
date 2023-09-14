# WordPress Headless intro

## Vad är WordPress Headless?

- WordPress Headless är en arkitektur för WordPress som separerar frontend från backend
- Frontend kan vara en webbapplikation, mobilapplikation eller IoT-applikation
- Backend är WordPress som fungerar som ett API
- WordPress Headless är en form av decoupled CMS
  - (Isärkopplat CMS)

## Skillnaden mellan vanliga WordPress och Headless

- Vanliga WordPress har en frontend och backend som är kopplade till varandra
- WordPress Headless har en frontend och backend som är separerade från varandra
- Frontend och backend kommunicerar med varandra via ett API
- Frontend kan vara en webbapplikation, mobilapplikation eller IoT-applikation

## Hur fungerar WordPress Headless?

- WordPress Headless fungerar genom att frontend kommunicerar med backend via ett API

## Fördelar med WordPress Headless

- Bättre prestanda och skalbarhet
- Flexibilitet i teknik och design
- Möjlighet till flera frontend-lösningar

## Nackdelar med WordPress Headless

- Ökad komplexitet för utvecklare
- Potentiell inlärningskurva för teamet

## Användningsområden för WordPress Headless

- Mobilapplikationer
- Internet of Things (IoT) integration
- Webbapplikationer (React, Vue, Angular, etc.)

## SEO och WordPress Headless

- När ni använder WordPress Headless så är det viktigt att ni tänker på SEO
- SEO-ansvaret ligger på de som bygger eventuell frontend webb

## Kom igång med WordPress Headless

### Testa WordPress REST API

1. Från och med WordPress version 4.7 finns ett inbyggt REST API. Se till att det är aktiverat på din webbplats genom att besöka `{DIN_WORDPRESS_URL}/wp-json/`.
   - Om du ser en JSON-utmatning är REST API aktiverat.

### WordPress REST API endpoints

- `/{wp-json}/wp/v2/posts` - Hämta alla inlägg
- `/{wp-json}/wp/v2/posts/{id}` - Hämta ett inlägg
- `/{wp-json}/wp/v2/pages` - Hämta alla sidor
- `/{wp-json}/wp/v2/pages/{id}` - Hämta en sida
- `/{wp-json}/wp/v2/categories` - Hämta alla kategorier

## Skapa egen endpoint

- Lägg till följande kod i `functions.php` i ditt WordPress-tema för att skapa egna endpoints
- Denna koden skapar två endpoints
  - `/{wp-json}/custom/menus` - Hämtar alla menyer
  - `/{wp-json}/custom/menus/{slug}` - Hämtar en specifik meny

```php
// Register custom REST API routes
add_action('rest_api_init', function () {
    register_rest_route('custom', '/menus', array(
        'methods' => 'GET',
        'callback' => 'get_menus',
    ));

    register_rest_route('custom', '/menus/(?P<slug>[a-zA-Z0-9-]+)', array(
        'methods' => 'GET',
        'callback' => 'get_menu',
    ));
});
```

## Skapa egen endpoint (forts.)

- Lägg till följande kod i `functions.php` i ditt WordPress-tema för att skapa egna endpoints
- Denna koden skapar callback-funktioner för att hämta menyer som används av våra endpoints

```php
// Callback for getting all menus
function get_menus()
{
    return get_nav_menu_locations();
}

// Callback for getting a specific menu
function get_menu($data)
{
    $menu_items = wp_get_nav_menu_items($data['slug']);
    return $menu_items;
}
```

## Skapa din Headless Frontend

1. Kör `npm create vue@latest` i terminalen för att skapa en ny Vue-applikation.
2. Anropa `/{wp-json}/custom/menus` med Postman för att se vilka IDn dina menyer har.
   - Kom ihåg ett ID för att använda i nästa steg.
3. Uppdatera `src/App.vue`, `src/router/index.js` för att hämta och visa er meny.
4. Skapa en ny vy (`src/views/PageView.vue`) för att visa en sida från WordPress.
5. Installera dotenv (`npm install dotenv`) och skapa en `.env`-fil för att lagra URLn till er WordPress-installation.

## `.env`

- Skapa en `.env`-fil i root-mappen för din frontend-applikation.
- Lägg till följande kod i `.env`-filen och ersätt URLn med URLn till din WordPress-installation.
- URLn ska sluta med `/wp-json`.
- Testa att besöka URLen i webbläsaren för att se att den fungerar.

### Exempel

```env
VITE_WP_JSON=http://localhost/wordpress/wp-json
```

## `src/App.vue`

```html
<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'

// Function to fetch menu items from the API
async function fetchMenuItems() {
  const response = await fetch(import.meta.env.VITE_WP_JSON + '/custom/menus/10');
  let data = await response.json();

  // Filter only the menu items that are pages
  menuItems.value = data.filter(item => item.object === 'page');;
}

const menuItems = ref([]);

onMounted(fetchMenuItems);
</script>
```

## `src/App.vue` (forts.)

```html
<template>
  <header>
    <div class="wrapper">
      <nav v-if="menuItems">
        <RouterLink v-for="item in menuItems" :key="item.ID" :to="item.object_id">
          {{ item.title }}
        </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>
```

## `src/router/index.js`

```js
import { createRouter, createWebHistory } from 'vue-router'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home', // Home kan ni lämna tom eller uppdatera hur ni vill
      component: () => import('../views/HomeView.vue')
    },
    {
      path: '/:id',
      name: 'page-post',
      component: () => import('../views/PageView.vue')
    }
  ]
})

export default router
```

## `src/views/PageView.vue`

```html
<script setup>
import { onMounted, ref } from 'vue';
import { onBeforeRouteUpdate, useRoute } from 'vue-router';

// Function to fetch menu items from the API
async function fetchPost(id) {
  const response = await fetch(import.meta.env.VITE_WP_JSON + '/wp/v2/pages/' + id);
  post.value = await response.json();
}

const route = useRoute();
const post = ref(false);

// Watch for route changes
onBeforeRouteUpdate(async (to, from, next) => {
  await fetchPost(to.params.id);
  next();
});

onMounted(async () => { await fetchPost(route.params.id); });
</script>
```

## `src/views/PageView.vue` (forts.)

```html
<template>
  <main>
    <div class="wrapper" v-if="post">
      <h1>{{ post.title.rendered }}</h1>
      <div v-html="post.content.rendered"></div>
    </div>
  </main>
</template>
```

## Testa och optimera

1. Testa din WordPress Headless-webbplats noggrant på olika enheter och webbläsare för att säkerställa att allt fungerar korrekt.
2. Optimera din frontend och server för bättre prestanda och användarupplevelse.

## Publicera din WordPress Headless-webbplats

1. När du är nöjd med din WordPress Headless-webbplats är det dags att publicera den.
2. Ladda upp frontend-applikationen på en webbserver eller en molnplattform och se till att din WordPress-installation är tillgänglig via REST API.

## Övningar

- Skapa en WordPress Headless-webbplats med en frontend-applikation i React, Vue, Angular eller Svelte.
- Visa din meny, dina sidor, dina inlägg, och din egna posttyp.
- Skapa en anpassad endpoint som hämtar både inlägg och sidor.
- Anropa din anpassade endpoint från din frontend-applikation och visa inlägg och sidor i en lista.
