# Ruby on Rails with Postgres 14.2, Redis, and Selenium

This is a Dockerfile and docker-compose.yml for running a Ruby on Rails application with Postgres 14.2, Redis, and Selenium. This is designed to be used as a starting point for a new Railes project and is not meant for
production use. It's meant to be an easy to use development environment for Ruby on Rails.

## Dockerfile Description

The Dockerfile in this project is used to create a Docker image with Ruby, Node.js, npm, and yarn installed.

Here's a breakdown of what each section does:

1. `FROM --platform=linux/amd64 ruby:3.3.0`: This line specifies the base image that we're using. In this case, it's the official Ruby 3.3.0 image for the linux/amd64 platform.

2. The `RUN apt-get update && apt-get install -y \` command updates the package lists for upgrades and new package installations. Then it installs the necessary dependencies for running Rails and RubyGems.

3. `RUN mkdir -p /app` and `WORKDIR /app`: These lines create a new directory `/app` in the Docker image and set it as the working directory. All subsequent commands in the Dockerfile will be run from this directory.

4. `RUN rm -rf node_modules`: This line deletes the node_modules folder if it exists.

5. `COPY Gemfile* ./`: This line copies the Gemfile and Gemfile.lock from your project into the Docker image.

6. `RUN gem install bundler && bundle install --jobs 20 --retry 5`: This line installs Bundler, a Ruby dependency manager, and then uses it to install the Ruby dependencies specified in your Gemfile.

7. `RUN gem install foreman`: This line installs Foreman, a manager for Procfile-based applications.

8. `COPY . /app`: This line copies the rest of your project into the Docker image.

9. `RUN rm -rf tmp/*`: This line removes all files in the tmp directory if it exists.

10. `ADD . /app`: This line adds the content of your Docker client's current directory (i.e., everything in your project) into the Docker image.

## Getting Started

To build the Docker image, run:

```bash
docker build -t my-ruby-app .

To run the Docker image, run:

docker run -it --name my-running-app my-ruby-app

Replace my-ruby-app with whatever you want to name your Docker image and container.