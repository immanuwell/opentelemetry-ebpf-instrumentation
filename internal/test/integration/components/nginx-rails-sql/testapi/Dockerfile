FROM ruby:4.0.5@sha256:bd5075f77ac998fa5b61e37842717d1a29482b0e02ab74e2a2a8ae371d121b32 AS builder

# Set the working directory to /build
WORKDIR /build

# Copy the source code into the image for building
COPY . .

RUN apt-get update && apt-get install -y default-libmysqlclient-dev

# Install Rails 
RUN gem install rails
RUN gem install bundler rails
RUN bundle install

EXPOSE 3040

FROM ruby:4.0.5-slim@sha256:86a2ff44ce474c1c9bd11dfb2fd7fe5408a5bfe8236b9bc6013e2c6ef4c02d39

RUN apt-get update && apt-get install -y default-libmysqlclient-dev

WORKDIR /
COPY --from=builder /build .
COPY --from=builder /usr/local/bundle /usr/local/bundle

# Run the app
CMD [ "rails", "server", "-p", "3040", "-b", "0.0.0.0" ]
