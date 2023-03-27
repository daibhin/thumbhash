# ThumbHash Ruby
## Introduction
The `thumbhash` library implements the
[Thumbhash](https://evanw.github.io/thumbhash/) image placeholder generation
algorithm invented by [Evan Wallace](https://madebyevan.com/) in Ruby.

A full explanation and interactive example of the algorithm can be found at [https://evanw.github.io/thumbhash/](https://evanw.github.io/thumbhash/)

The ideal use case is to store the very compact binary hash representation of an image so that a placeholder image can be can be generated clientside while the original image loads asynchronously.

## Usage
Using the [MiniMagick](https://github.com/minimagick/minimagick) library to process the image, this example shows how to generate a thumb hash that can be stored alongside an image as well as the method to convert the hash into a data string for the image placeholder.
```ruby
require "../lib/thumbhash"
require "mini_magick"

image = MiniMagick::Image.open("flower.jpg")

rgba_pixels = image.get_pixels("RGBA").flatten

# Generate the binary hash
binary_thumb_hash = ThumbHash.rgba_to_thumb_hash(
  image.width,
  image.height,
  rgba_pixels
)

# Generate the placeholder image data
ThumbHash.thumb_hash_to_data_url(binary_thumb_hash)
```