# NestJS Serverless Monorepo Example

Example integrated NX monorepo with two NestJS apps served locally and deployed via Serverless Framework.

## Setup
1. `npm ci`
2. A configured AWS account with credentials if planning to deploy.
   1. [Docs for setting up AWS credentials.](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files)
   2. Update `provider.profile` in `serverless.base.yml` if using a non-default AWS CLI profile.

## Local Dev
1. `nx run-many --target=serve` or `nx serve api1` or `nx serve api2`
   1. `https://localhost:3000/dev/test/`
   2. `https://localhost:3001/dev/test/`

## Deploy
1. `nx run-many --target=deploy` or `nx deploy api1` or `nx deploy api2`
   1. `https://<api-id>.execute-api.us-east-1.amazonaws.com/dev/test/`

## Notes
* The default `serve` target in `project.json` has been updated to use `serverless offline`.
* A `deploy` target was added.
* Several packages were ignored via `custom.bundle.ignorePackages` in `serverless.base.yml` for it to build successfully. This [thread](https://github.com/nestjs/nest/issues/1706) provides background.
* Bundled size: ~500kb + ~750kb .map file
* `custom.bundle.esbuild=true` in `serverless.base.yml` does not work.
