# Cloud Agent base image for this Jekyll (GitHub Pages) blog.
#
# Ruby is pinned to 2.7 on purpose. The site targets the GitHub Pages
# toolchain (jekyll 3.9 / github-pages ~214), which pulls in liquid 4.0.3
# and pathutil 0.16.2. Those gems rely on behavior removed in newer Ruby:
#   - liquid 4.0.3 calls Object#tainted?, removed in Ruby 3.2 -> build fails.
#   - pathutil 0.16.2 passes a Hash as a positional arg to File.read, which
#     raises under Ruby 3.x -> `jekyll serve --watch/--livereload` fails.
# Ruby 2.7 is what GitHub Pages itself runs, so it keeps the pinned
# toolchain working for both `jekyll build` and the watching dev server.
FROM ruby:2.7

# git and curl are needed for source checkout and health checks; the
# build-essential toolchain lets native gems (ffi, sassc, nokogiri, ...)
# compile when a prebuilt platform gem is unavailable.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        curl \
        build-essential \
    && rm -rf /var/lib/apt/lists/* \
    && gem install bundler -v "~> 2.4" --no-document

WORKDIR /workspace
