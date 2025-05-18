# Addtl Backend Tools
## Setting up Swagger
Nestjs has a swagger module, so setup was super easy. 

```bash
npm install --save @nestjs/swagger
```

And then import the swagger module and update the bootstrap function in `main.ts`

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

	// swagger setup
  const config = new DocumentBuilder()
    .setTitle('Cats example')
    .setDescription('The cats API description')
    .setVersion('1.0')
    .addTag('cats')
    .build();
  const documentFactory = () => SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api', app, documentFactory);

  await app.listen(process.env.PORT ?? 3000);
}
bootstrap();
```

Run the dev server and navigate to `localhost:3000/api` to see the generated docs.

## Docker Setup
If I ever do pick up any help with my app I would consider setting up a dockerfile/compose to set up a postgres db in a container vs running postgres locally. But since I already have a local pg db I am happy with that for now.