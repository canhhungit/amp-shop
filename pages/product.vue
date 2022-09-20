<template>
  <div class="item-view view" vocab="https://schema.org/" typeof="Product">
    <div class="item-view-header">
      <a :href="product_data.url_path" target="_blank">
        <h1 property="name">{{ product_data.name }}</h1>
      </a>
      <!-- <span v-if="item.url" class="host"> ({{ item.url | host }}) </span> -->
      <p class="meta" property="aggregateRating" typeof="AggregateRating">
        <span property="ratingValue">{{ product_data.rating_average }}</span
        >/<span property="bestRating">5</span> points (
        <span property="ratingCount">{{ product_data.review_count }}</span> đánh giá)
      </p>
      <div property="offers" typeof="Offer">
        <span property="price">{{ product_data.price }}</span
        ><span property="priceCurrency" content="VND">đ</span>
        <link property="availability" href="https://schema.org/InStock" />Còn hàng
      </div>
    </div>
    <div class="item-view-comments">
      <amp-carousel
        id="carouselWithPreview"
        class="mb3"
        width="400"
        autoplay
        height="300"
        delay="3000"
        layout="responsive"
        type="slides"
        on="slideChange:carouselWithPreviewSelector.toggle(index=event.index, value=true)"
      >
        <amp-img
          v-for="image in product_data.images"
          :key="image.base_url"
          rel="image"
          :src="image.base_url"
          width="500"
          height="500"
          layout="responsive"
          alt="a sample image"
        />
      </amp-carousel>
      <amp-selector
        id="carouselWithPreviewSelector"
        class="carousel-preview center"
        on="select:carouselWithPreview.goToSlide(index=event.targetOption)"
        layout="container"
      >
        <amp-img
          v-for="(image, index) in product_data.images"
          :key="image.base_url"
          :option="index"
          :src="image.base_url"
          width="40"
          height="40"
          style="margin:0 5px"
          alt="a sample image"
        />
      </amp-selector>
    </div>

    <div class="item-view-comments">
      <p class="item-view-comments-header">
        Mô tả sản phẩm
      </p>
      <ul class="comment-children">
        <li v-if="source == 'shopee'" class="comment">
          <pre property="description" v-html="product_data.description" />
        </li>
        <li v-else class="comment" property="description" v-html="product_data.description" />
      </ul>
    </div>

    <div class="footer">
      <div class="width-50">
        Theo dõi giá
      </div>
      <div class="width-50 footer-buynow">
        Mua ngay
      </div>
    </div>
  </div>
</template>

<script>
import { getProduct } from '../libs/apiClient'

export default {
  layout: 'productLayout',
  components: {},

  data() {
    return {
      product: null,
      product_data: null,
      source: null
    }
  },

  async asyncData() {
    const product = await getProduct(1)
    let product_data = product.product_data

    let source = product.product_data.source
    return {
      product,
      product_data,
      source
    }
  }
}
</script>

<style lang="scss">
.width-50 {
  width: 50%;
  padding: 10px;
}
.footer-buynow {
  background-color: #f00;
}
.footer {
  background-color: #bc8f8f;
  position: sticky;
  display: flex;
  height: 40px;
  left: 0;
  bottom: 0;
  width: 100%;
  color: #fff;
  text-align: center;
}
.mb3 {
  margin-bottom: 1.5rem;
}
.center {
  text-align: center;
}
pre {
  white-space: pre-wrap;
  word-wrap: break-word;
  font-size: 14px;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans,
    Helvetica Neue, sans-serif;
}
.item-view-header {
  background-color: #fff;
  padding: 1.8em 2em 1em;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  h1 {
    display: inline;
    font-size: 1.5em;
    margin: 0;
    margin-right: 0.5em;
  }
  .meta {
    a {
      text-decoration: underline;
    }
  }
}
.item-view-header .host,
.item-view-header .meta,
.item-view-header .meta a {
  color: #828282;
}
.item-view-comments {
  background-color: #fff;
  margin-top: 10px;
  padding: 0 2em 0.5em;
}
.item-view-comments-header {
  margin: 0;
  font-size: 1.1em;
  padding: 1em 0;
  position: relative;
  .spinner {
    display: inline-block;
    margin: -15px 0;
  }
}
.comment-children {
  list-style-type: none;
  font-size: 14px;
  text-align: justify;
  padding: 0;
  margin: 0;
}
.comment {
  border-top: 1px solid #eee;
  text-align: justify;
  font-size: 14px;
  position: relative;
  .by {
    color: #828282;
    a {
      color: #828282;
      text-decoration: underline;
    }
  }
  .text {
    overflow-wrap: break-word;
    a {
      &:hover {
        color: #f60;
      }
    }
    pre {
      white-space: pre-wrap;
    }
  }
  .toggle {
    background-color: #fffbf2;
    padding: 0.3em 0.5em;
    border-radius: 4px;
    a {
      color: #828282;
      cursor: pointer;
    }
    &.open {
      padding: 0;
      background-color: transparent;
      margin-bottom: -0.5em;
    }
  }
}
.comment .by,
.comment .text,
.comment .toggle {
  font-size: 0.9em;
  margin: 1em 0;
}
@media (max-width: 600px) {
  .item-view-header h1 {
    font-size: 1.25em;
  }
}
// @media {
// 	(max-width {
// 		&: {
// 			600px) {
// 				.item-view-header h1 {
//     font-size: 1.25em;
// 			}
// 		}
// 	}
// }
</style>
