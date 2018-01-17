# Singularity RStudio + Spark

Singularity image for [RStudio](https://www.rstudio.com/products/rstudio/) and
[Apache Spark](https://spark.apache.org/).

This is still a work in progress.

## Build

You can build a local Singularity image named `my_image.simg` with:

```sh
sudo singularity build my_image.simg Singularity
```

## Run Spark

### Master

You can launch a master instance of Spark with:

```sh
singularity exec my_image.simg \
  spark-class "org.apache.spark.deploy.master.Master"
```

### Worker

You can launch a worker instance of Spark with:

```sh
singularity exec my_image.simg \
  spark-class "org.apache.spark.deploy.worker.Worker"
```

## Run RStudio

You can launch an RStudio Server with:

```sh
singularity exec my_image.simg \
  rserver
```

## Contributing

Bug reports and pull requests are welcome on GitHub at
https://github.com/nickjer/singularity-rstudio-spark.

## License

The gem is available as open source under the terms of the [MIT
License](http://opensource.org/licenses/MIT).
