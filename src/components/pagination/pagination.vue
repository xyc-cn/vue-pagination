<template>
  <div v-bind:id="id"></div>
</template>
<script>

  import $ from './paginator.js';
  export default {
    props: ['current', 'total', 'url', 'callback'],
    data() {
      return {
        id: new Date().getTime()
      }
    },
    methods: {
      setPaginator: function () {
        var that = this;
        var currentPage = this.current ? this.current : 1;
        var total = this.total > 1 ? this.total : 1;
        if (currentPage > total) {
          currentPage = 1
        }
        var url = location.href;
        var options = {
          currentPage: currentPage,
          totalPages: total,
          onPageClicked: function (event, originalEvent, type, page) {
            originalEvent.preventDefault();
            event.preventDefault();
            that.callback && that.callback(page, that);
          },
          pageUrl: function (type, clickedPage, current) {
            return url;
          }
        };
        $('#' + that.id).bootstrapPaginator(options);
      }
    },
    watch: {
      current: "setPaginator",
      total: "setPaginator"
    },
    mounted: function () {
      if (this.total && this.total > 0) {
        this.setPaginator();
      }
    }
  }
</script>
<style>
  .button {
    -moz-appearance: none;
    -webkit-appearance: none;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    background-color: white;
    border: 1px solid #dbdbdb;
    border-radius: 3px;
    color: #363636;
    display: -webkit-inline-box;
    display: -ms-inline-flexbox;
    display: inline-flex;
    font-size: 14px;
    height: 32px;
    -webkit-box-pack: start;
    -ms-flex-pack: start;
    justify-content: flex-start;
    line-height: 24px;
    padding-left: 8px;
    padding-right: 8px;
    position: relative;
    vertical-align: top;
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    cursor: pointer;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    padding-left: 10px;
    padding-right: 10px;
    text-align: center;
    white-space: nowrap;
}
  .pagination .is-primary a{
    color: white;
  }
  .pagination ul {
    padding: 0;
    list-style: none;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-flex: 1;
    -ms-flex-positive: 1;
    flex-grow: 1;
    -ms-flex-negative: 0;
    flex-shrink: 0;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
}
.pagination li {
    margin: 0 2px;
    padding: 0;
}
.pagination a {
    display: block;
    min-width: 32px;
    color: #00d1b2;
    cursor: pointer;
    text-decoration: none;
    -webkit-transition: none 86ms ease-out;
    transition: none 86ms ease-out;
}
.button.is-primary {
    background-color: #00d1b2;
    border-width: 0;
    color: white;
}
</style>