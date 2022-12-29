---
title: Images
parent: Webdev
---

# Images

## Responsive
- <https://www.reddit.com/r/webdev/comments/ck3gzp/coming_back_to_frontend_dev_after_a_lot_of/>
- responsive image generator: <https://www.responsivebreakpoints.com/>
- responsive image linter: <https://ausi.github.io/respimagelint/>
- **img srcset**
  - Bilder je nach viewport-Breite laden
  - `<img src="default.jpg" srcset="small.jpg 320w, medium.jpg 600w, large.jpg 900w" alt="">`
  - <https://blog.kulturbanause.de/2014/09/responsive-images-srcset-sizes-adaptive/>
  - <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture>
  - <https://cloudfour.com/thinks/responsive-images-the-simple-way/>
  - <https://css-tricks.com/beyond-media-queries-using-newer-html-css-features-for-responsive-designs/>
- content aware resizing
  - <https://trekhleb.dev/blog/2021/content-aware-image-resizing-in-javascript/>
- <https://css-tricks.com/images-are-hard/>
- <https://jakearchibald.com/2021/serving-sharp-images-to-high-density-screens/>


## Performance
- <https://web.dev/fast/#optimize-your-images> (google)
- <https://userinterfacing.com/the-fastest-way-to-increase-your-sites-performance-now/>
- <https://cssauthor.com/image-optimization-tools/>
- sprite sheets (funktioniert auch mit SVGs) => weniger Requests, HTTP2 könnte heutzutage aber besser sein
- **svgo**
  - *Node.js tool for optimizing SVG files*
  - <https://github.com/svg/svgo>
- **Formate**
  - Vergleich
    - <https://jakearchibald.com/2020/avif-has-landed/>
    - <https://cloudinary.com/blog/time_for_next_gen_codecs_to_dethrone_jpeg>
  - jpeg 2000
  - jpeg XR
  - jpeg XL
  - webp
    - <https://css-tricks.com/using-webp-images/>
    - <https://caniuse.com/#feat=webp>
    - z.T. bessere Komprimierung als jpg
    - ```html
    <picture>
      <source srcset="image.webp" type="image/webp"/>
      <img src="image.jpg" type="image/jpeg"/> <!-- fallback for older browsers -->
    </picture>
    ```
  - webp2
  - avif
    - av1 still image format
    - *AVIF generally has better compression than WebP, JPEG, PNG and GIF and is designed to supersede them.*
    - Stand 11.8.20 schlechter [Browser-Support](https://caniuse.com/#feat=avif)
      <img src="https://caniuse.bitsofco.de/image/avif.jpg" width="600" loading="lazy"/>
    - <https://darekkay.com/blog/avif-images/> (12.4.21)
  - heif
    - high efficiency image file format
    - Stand 7.9.20 kein Browser-Support
    - <https://caniuse.com/heif>
  - heic

### Lazy Loading
- <https://web.dev/native-lazy-loading>
- <https://caniuse.com/#feat=loading-lazy-attr>
- <https://i.redd.it/mxvgofswmfk21.png>
- <https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/>
- <https://www.stefanjudis.com/today-i-learned/how-to-preload-responsive-images-with-imagesizes-and-imagesrcset/>
- **low quality image placeholders (LQIP)**
  - <https://github.com/transitive-bullshit/lqip-modern>
  - <https://www.reddit.com/r/javascript/comments/blqn1q/image_lazy_loading_with_inline_svg/>
  - <https://css-tricks.com/tips-for-rolling-your-own-lazy-loading/>

### Kompression und Konverter
- <https://squoosh.app/>
  - PWA; kann avif und webp
- <https://github.com/google/guetzli/>
- **sharp**
  - <https://github.com/lovell/sharp>
- **google/libwebp**
  - <https://developers.google.com/speed/webp/docs/using>
  - konvertiert jpg/png zu webp
  - `cwebp -q 80 input.png -o output.webp`
- **imagemin**
  - cli & npm
  - <https://www.npmjs.com/package/imagemin>
  - diverse Plugins
    - z.b. für [webp](https://www.npmjs.com/package/imagemin-webp)
- **gulp-webp**
  - <https://github.com/sindresorhus/gulp-webp>


## SVG
- <https://github.com/jakearchibald/svgomg> (compressor)
