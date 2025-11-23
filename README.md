# Entity and Resource Generator Guide

This repository exposes two code-generation scripts that keep the NestJS backend and hexagonal domain layer in sync with a Prisma schema.
Structure inspired by [NestJS boilerplate of brocoders](https://github.com/brocoders/nestjs-boilerplate/tree/main).
Make sure to adapt the paths and module names in the scripts if you integrate them into your own project.

## Prerequisites

- **Node.js 20+**
- **PostgreSQL client headers** (only required if you plan to run Prisma against a live database).
- Run `pnpm install` once to pull in dev dependencies such as `ts-node` and `tsconfig-paths`, which the generators rely on.

## Scripts overview

| Script                  | Entry Point                                     | Description                                                                                                                             |
| ----------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `pnpm generate:typeorm` | `generate-typeorm-entities.ts`    | Reads `schema.prisma` and emits TypeORM-compatible entity classes under `src/database/prisma/entities`.             |
| `pnpm generate:hex`     | `generate-hexagonal-resources.ts` | Builds DTOs, repositories, mappers, and enums in `src/prisma-generated` and `libs/shared` based on the same schema. |

Both scripts are idempotent and safe to run whenever the Prisma schema changes.

## Usage

1. Install dependencies (once per clone):

   ```bash
   pnpm install
   ```

2. Generate or refresh the TypeORM entities:

   ```bash
   pnpm generate:typeorm
   ```

3. Generate or refresh the hexagonal resources:

   ```bash
   pnpm generate:hex
   ```

The commands can be executed independently, but you will usually run both sequentially after modifying anything in `schema.prisma`.
