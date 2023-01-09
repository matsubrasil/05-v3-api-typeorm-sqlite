### Aprendizado - Realizar migrations com Typeorm v0.3

Marius Espejo <br>

TypeORM v0.3.x Migrations, queries, with NestJS! <br>
https://www.youtube.com/watch?v=5G81_VIjaO8&list=WL&index=2 <br>

### Antes de tudo, gerar o módulo users

Criar todos os CRUDs do user, assim, quando rodar a migration, o sistema reconhecerá a entidade user.

### Criar uma pasta na raiz do projeto

Pasta na raiz ./db <br>
Nesta pasta ficam o data-source.ts e as migrations.

### Configuração

> Criar arquivo data-source.ts na pasta ./db

```typescript
import { DataSource, DataSourceOptions } from 'typeorm';

export const dataSourceOptions: DataSourceOptions = {
  type: 'sqlite',
  database: 'db.sqlite',
  entities: ['dist/**/*.entity.js'],
  migrations: ['dist/**/migrations/*.js'],
};

const dataSource = new DataSource(dataSourceOptions);

export default dataSource;
```

### Ajustar AppModule com importação do DataSource

```javascript
@Module({
  imports: [TypeOrmModule.forRoot(dataSourceOptions), UsersModule],
  controllers: [AppController],
  providers: [AppService],
})
```

### Package JSON

```JSON
  "typeorm": "npm run build && npx typeorm -d dist/db/data-source.js",
  "migration:generate": "npm run typeorm -- migration:generate",
  "migration:run": "npm run typeorm -- migration:run",
  "migration:revert": "npm run typeorm -- migration:revert"
```

### Executar comando de gerar migration

> npm run migration:generate -- src/db/migrations/CreateUsers

### Executar a migration

> npm run migration:run
