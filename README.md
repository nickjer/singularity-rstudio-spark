# Singularity Apache Spark w/ RStudio Server

Singularity image for [Apache Spark] with the [sparklyr] package installed.
This image has an [RStudio Server] base for launching an RStudio Server to
connect with an Apache Spark cluster running in Standalone Mode.

[Apache Spark]: https://spark.apache.org/
[sparklyr]: http://spark.rstudio.com/
[RStudio Server]: https://www.rstudio.com/products/rstudio/

This is still a work in progress.

## Build

You can build a local Singularity image named `singularity-rstudio-spark.simg`
with:

```sh
sudo singularity build singularity-rstudio-spark.simg Singularity
```

## Deploy

Instead of building it yourself you can download the pre-built image from
[Singularity Hub](https://www.singularity-hub.org) with:

```sh
singularity pull --name singularity-rstudio-spark.simg shub://nickjer/singularity-rstudio-spark
```

## Run

You can launch Spark in [Standalone Mode] by first launching a "master" process
which will print out a `spark://HOST:PORT` for itself, which you can then use
to connect "workers" to it.

[Standalone Mode]: https://spark.apache.org/docs/latest/spark-standalone.html

### Spark Master

You can launch a "master" process as a Singularity app with:

```sh
singularity run --app spark-master singularity-rstudio-spark.simg
```

### Worker

You can launch a "worker" process as a Singularity app with:

```sh
singularity run --app spark-worker singularity-rstudio-spark.simg
```

## Contributing

Bug reports and pull requests are welcome on GitHub at
https://github.com/nickjer/singularity-rstudio-spark.

## License

The code is available as open source under the terms of the [MIT License].

[MIT License]: http://opensource.org/licenses/MIT
