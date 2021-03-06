# fastify-website

[![CircleCI](https://circleci.com/gh/lmammino/fastify-website.svg?style=shield)](https://circleci.com/gh/lmammino/fastify-website)

This project is used to build the website for [fastify web framework](https://github.com/fastify/fastify) and publish it online.


## Requirements

 - Node 8.3.0+
 - Install dependencies with `npm install`


## Build

To trigger the build of the website you just need to run:

```bash
npm run build
```

This will execute all the steps necessary to create a build (static website).

If you are developing you can run:

```bash
npm start
```

This will trigger the build and also start a live server that will allow you to visualize the changes you are performing on the website.

(note that every time you make a change to the assets that constitutes the content of the website you will need to launch `npm run build:website` to trigger a rebuild)


## Build steps

In case you are interested in knowing more about how the build process works, here are the main steps that are performed during its execution:

  1. **Cleanup**: removes temporary resources that might have created from a previous build
  2. **Temp folders creation**: Creates the needed folders for the build process
  3. **Get releases**: uses the GitHub APIs to download the latest releases of Fastify so that the documentation pages can be regenerated dynamically.
  4. **Process releases**: processes the releases creating all the necessary dynamic files that are derivate from the original fastify releases (mostly used to generate and process documentation pages)
  5. **Website generation**: uses [Metalsmith](http://www.metalsmith.io/) to compile a static version of the website.

Checkout the [Package scripts](package.json) to understand which files trigger these actions in case you want to have a look at the code for any of the steps described above.


## Publishing

The publishing of the website is performed automatically through Circle CI (in a Continuous Delivery fashion).

Every time there's a change on master, if the build was created successfully, then it is automatically published on an S3 Bucket.

In order for this to work, Circle CI will need to be configured correctly providing all the necessary environment variables:

 - `BUCKET_NAME`: the name of the S3 bucket that hosts the website (the bucket needs to be already configured to serve static files)
 - `AWS_ACCESS_KEY_ID`: AWS access key of the machine user that has the rights to write files in the previously defined S3 bucket
 - `AWS_SECRET_ACCESS_KEY`: Secret access key for the key specified above


## Contributing

Everyone is very welcome to contribute to this project.
You can contribute just by submitting bugs or suggesting improvements by
[opening an issue](issues) or by [sending a pull request](pulls).


## License
Licensed under [MIT License](LICENSE). © Luciano Mammino.
