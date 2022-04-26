<script>
export default {
  name: 'PicItem',
  props: {
    item: {
      type: Object,
      required: true,
    },
    parentIsShow: Boolean,
  },
  render(h) {
    return h(
      'div',
      {
        class: "gutter",
        domProps: {
          innerHTML:`
            ${this.item.website 
              ? `<a class="pic__link" href="${this.item.website}" target="_blank">` 
              : ''
            }
                <div class="imgContainer">
                  <img
                    loading="lazy"
                    class="img-resp"
                    src="${this.item.imageUrl ? `https://cloud.culture.tw${this.item.imageUrl}`:''}"
                    alt="${this.item.actName}"
                  />
                </div>
                <div class="pic__intro">
                  <div class="pic__tag">
                    倒數<span>${ this.item.countDown }</span
                    >天
                  </div>
                  <h2 class="pic__tit">${ this.item.actName }</h2>
                  <div class="pic__dist">
                    ${this.parentIsShow 
                      ? `<p class="pic__city">${ this.item.place[0] }</p>` 
                      : ''
                    }
                    <p class="pic__town">
                      ${ this.item.place[1] 
                        ? this.item.place[1] 
                        : '' 
                      }
                    </p>
                  </div>
                  <p class="pic__date">
                    ${ this.makeDateStr(this.item.startTime) } ~ ${ this.makeDateStr(this.item.endTime) }
                  </p>
                </div>
            ${this.item.website 
              ? '</a>' 
              : ''
            }
          `,
        }
      },
    )
  },
  methods: {
    makeDateStr(date){
      return `${new Date(date).getFullYear()}/${new Date(date).getMonth() + 1}/${new Date(date).getDate()}`
    }
  }
}
</script>


<style>
  .pic__item {
    width: 33.3333%;
    padding: 12px;
    box-sizing: border-box;
  }

  .pic .gutter {
    position: relative;
    background-color: #fff;
    height: 100%;
  }

  .pic__intro {
    margin: 12px;
    color: #000;
  }

  .pic__tag {
    position: absolute;
    top: 12px;
    right: 12px;
    width: 40px;
    padding-top: 8px;
    padding-bottom: 8px;
    font-size: 14px;
    text-align: center;
    color: rgba(255, 255, 255, 0.63);
    background-color: #bf0915c4;
  }

  .pic__tag span {
    font-size: 22px;
    color: #fff;
    width: fit-content;
    margin: 0px auto;
    display: block;
  }

  .pic__tit {
    margin: 12px 0 5px 0;
    font-size: 1.2rem;
    font-weight: normal;
    transition: color 0.5s ease-in-out;
  }

  .pic__dist {
    display: flex;
    align-items: center;
    margin-top: 5px;
    margin-bottom: 5px;
  }

  .pic__city,
  .pic__town,
  .pic__date {
    margin: 0;
    font-size: 14px;
  }

  .pic__city {
    padding: 0px 5px;
    color: #fff;
    margin-right: 5px;
    background-color: #aaa;
  }
  .imgContainer {
    position: relative;
  }
  .imgContainer::after {
    content: "";
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #cc0000;
    opacity: 0;
    display: block;
    transition: opacity 0.5s ease-in-out;
  }

  .pic__date {
    color: #b3b3b3;
  }
  .pic__link {
    text-decoration: none;
  }
  .pic__link:hover .pic__tit {
    color: #cc0000;
  }

  .pic__link:hover .imgContainer::after {
    opacity: 0.4;
  }

  .pic .img-resp {
    aspect-ratio: 16 / 9;
    object-fit: cover;
    object-position: center;
    transition: all 0.5s ease-in-out;
  }
</style>
