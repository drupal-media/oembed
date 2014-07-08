# Drupal 8 oEmbed module specfication

I would love to build something on top of https://github.com/felixgirault/essence that handles the heavy work for us. https://github.com/kayue/KayueEssenceBundle might also be of interest.

## Base components
* Drupal Caching layer for Essence library
* UI to enable/order/configure providers (oembed.providers.yml)
* Twig templates (and corresponding theme functions) for the various different types of oEmbed items.

## Field components
* Widget and formatters for core link field
* Widget and formatters for core file field
* Widget and formatters for core image field (restricted to oEmbed responses of type 'photo' or mime type image/oembed)
* Common widget options:
  * Allowed oEmbed types (photo/video/link/rich)
  * Allowed oEmbed providers?
* Common formatter options:
  * Maximum width
  *Maximum height
* Second formatter for thumbnail?

## Filter components
* Filter and corresponding CKEditor button for embedding an oEmbed URL, stored using a data attribute:
  
  ```html
  <div data-oembed-url="https://www.youtube.com/watch?v=dQw4w9WgXcQ" data-max-width="500" data-max-height="100 />
  ```
  
  Basically keep this as simple as possible. The embed should have the output go through the Twig templates for the different types: image/video/rich/url.
* A separate oembed_url filter that performs simple replacement of URLs:
  
  ```html
  $text = $essence->replace($text, function($media) {
    return theme('oembed__' . $media->type, $media);
  }
