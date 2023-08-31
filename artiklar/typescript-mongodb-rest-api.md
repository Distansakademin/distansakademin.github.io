# Typescript & Mongodb REST-API

Komplett guide för att skapa ett REST API med avancerad Typescript och MongoDB.

1. Installera Node.js och Typescript:
   - Se till att du har Node.js installerat på din dator. Du kan ladda ner det från den officiella Node.js webbplatsen.
   - För att arbeta med Typescript, installera det globalt genom att köra följande kommando i terminalen:\
   `npm install -g typescript`

2. Skapa ett projekt:
   - Skapa en ny mapp för ditt projekt och navigera till den genom att köra kommandot: \
   `mkdir mitt-rest-api && cd mitt-rest-api`
   - När du är inne i projektmappen, initiera ett nytt Node.js-projekt genom att köra \
   `npm init -y`

3. Konfigurera Typescript:
   - Skapa en `tsconfig.json`-fil i rotmappen för ditt projekt.
   - Lägg till följande konfiguration i `tsconfig.json`:

     ```json
     {
       "compilerOptions": {
         "target": "es6",
         "module": "commonjs",
         "outDir": "dist",
         "sourceMap": true
       },
       "include": [
         "src/**/*.ts"
       ],
       "exclude": [
         "node_modules"
       ]
     }
     ```

4. Installera nödvändiga bibliotek:
   - Installera de nödvändiga biblioteken för att bygga REST API:et genom att köra följande kommando: \
   `npm install express mongoose @types/express @types/mongoose`

5. Konfigurera Express:
   - Skapa en `src`-mapp i rotmappen för ditt projekt och navigera till den: `mkdir src && cd src`
   - Inuti `src`-mappen, skapa en `index.ts`-fil och konfigurera en grundläggande Express-server:

     ```typescript
     import express, { Application, Request, Response } from 'express';

     const app: Application = express();
     const port = 3000;

     app.use(express.json());

     app.listen(port, () => {
       console.log(`Server körs på port ${port}`);
     });
     ```

6. Anslut till MongoDB:
   - Installera MongoDB-drivrutinen för Node.js genom att köra: `npm install mongodb`
   - Importera `mongodb`-modulen och anslut till din MongoDB-databas i `index.ts`:

     ```typescript
     import { MongoClient, Db, Collection, ObjectId } from 'mongodb';

     const uri = 'mongodb://localhost:27017';
     const dbName = 'mittDatabase';

     let db: Db;
     let usersCollection: Collection;

     const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true });

     client.connect((err) => {
       if (err) {
         console.error('Misslyckades med anslutning till MongoDB:', err);
       } else {
         console.log('Ansluten till MongoDB');
         db = client.db(dbName);
         usersCollection = db.collection('users');
       }
     });
     ```

7. Lägg till CRUD-operationer:
   - Inuti `client.connect`-callbacken kan du börja definiera dina REST API-rutter och deras motsvarande logik.
   - Låt oss skapa exempel på rutter för CRUD-operationer (Create, Read, Update, Delete) för en MongoDB-samling som kallas `users`:

     ```typescript
     // Hämta alla användare
     app.get('/users', async (req: Request, res: Response) => {
       try {
         const allUsers = await usersCollection.find({}).toArray();
         res.json(allUsers);
       } catch (error) {
         console.error('Misslyckades med att hämta användare:', error);
         res.status(500).json({ error: 'Misslyckades med att hämta användare' });
       }
     });

     // Skapa en ny användare
     app.post('/users', async (req: Request, res: Response) => {
       const newUser = req.body;
       try {
         const result = await usersCollection.insertOne(newUser);
         res.json(result.ops[0]);
       } catch (error) {
         console.error('Misslyckades med att skapa användare:', error);
         res.status(500).json({ error: 'Misslyckades med att skapa användare' });
       }
     });

     // Uppdatera en användare
     app.put('/users/:id', async (req: Request, res: Response) => {
       const userId = req.params.id;
       const updatedUser = req.body;
       try {
         const result = await usersCollection.updateOne({ _id: new ObjectId(userId) }, { $set: updatedUser });
         res.json(result);
       } catch (error) {
         console.error('Misslyckades med att uppdatera användare:', error);
         res.status(500).json({ error: 'Misslyckades med att uppdatera användare' });
       }
     });

     // Ta bort en användare
     app.delete('/users/:id', async (req: Request, res: Response) => {
       const userId = req.params.id;
       try {
         const result = await usersCollection.deleteOne({ _id: new ObjectId(userId) });
         res.json(result);
       } catch (error) {
         console.error('Misslyckades med att ta bort användare:', error);
         res.status(500).json({ error: 'Misslyckades med att ta bort användare' });
       }
     });
     ```

8. Bygg och kör applikationen:
   - Gå tillbaka till rotmappen för ditt projekt.
   - Kompilerar Typescript-koden till JavaScript genom att köra: `tsc`
   - Starta servern genom att köra: `node dist/index.js`
   - Besök `http://localhost:3000/users` i din webbläsare eller använd verktyg som Postman för att testa APIet.

## Uppgift / övning

Skapa ett REST API med Typescript och MongoDB för att hantera en samling av produkter. Produkterna ska ha följande egenskaper:

- `id` (string)
- `name` (string)
- `price` (number)
- `description` (string)
- `imageUrl` (string)
- `inStock` (boolean)
- `category` (string)
- `tags` (string[])

APIet ska ha följande routes:

- `GET /products` - Hämta alla produkter
- `GET /products/:id` - Hämta en specifik produkt
- `POST /products` - Skapa en ny produkt
- `PUT /products/:id` - Uppdatera en produkt
- `DELETE /products/:id` - Ta bort en produkt
- `GET /products/categories` - Hämta alla kategorier
- `GET /products/categories/:category` - Hämta alla produkter i en specifik kategori
- `GET /products/tags` - Hämta alla taggar
- `GET /products/tags/:tag` - Hämta alla produkter med en specifik tagg
- `GET /products/search` - Sök efter produkter

## Länkar

- [Express](https://expressjs.com/)
- [MongoDB](https://www.mongodb.com/)
- [MongoDB Node.js Driver](https://mongodb.github.io/node-mongodb-native/)
- [Typescript](https://www.typescriptlang.org/)

