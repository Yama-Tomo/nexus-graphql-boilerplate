# Migration `20200828032157-first`

This migration has been generated by yamaya_tomohiro at 8/28/2020, 12:21:57 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE `hoge`.`User` (
`id` int  NOT NULL  AUTO_INCREMENT,
`name` varchar(191)  NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `hoge`.`Post` (
`id` int  NOT NULL  AUTO_INCREMENT,
`title` varchar(191)  NOT NULL ,
`content` varchar(191)  ,
`published` boolean  NOT NULL ,
`userId` int  ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

ALTER TABLE `hoge`.`Post` ADD FOREIGN KEY (`userId`) REFERENCES `hoge`.`User`(`id`) ON DELETE SET NULL ON UPDATE CASCADE
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20200828032157-first
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,22 @@
+generator client {
+  provider = "prisma-client-js"
+}
+
+datasource db {
+  provider = "mysql"
+  url = "***"
+}
+
+model User {
+  id          Int      @default(autoincrement()) @id
+  name        String
+  posts       Post[]
+}
+
+model Post {
+  id          Int      @default(autoincrement()) @id
+  title       String
+  content     String?
+  published   Boolean
+  author      User?
+}
```

