<template>
  <aside :class="{'show':isAsideShow}">
    <div class="brand">
      <div @click="toggleAside(false)" class="logo">
        <router-link to="/" exact>
          <img class="vue-logo" src="./../../assets/img/v-logo.png">
          <img class="bootstrap-logo" src="./../../assets/img/b-logo.png">
        </router-link>
      </div>
      <h2 @click="toggleAside(false)" class="text-center">
        <router-link to="/" exact>uiv</router-link>
      </h2>
    </div>
    <div class="nav-container">
      <div class="nav-div">
        <ul class="nav nav-pills nav-stacked" role="tablist">
          <template v-for="item in asideItems">
            <template v-if="item.items">
              <li role="presentation" class="no-link">
                <a role="button">
                  {{item.label}}
                </a>
              </li>
              <li role="presentation" v-for="_item in item.items" @click="toggleAside(false)">
                <router-link :to="_item.path" role="button" class="sub-list">
                  {{_item.label}}
                </router-link>
              </li>
            </template>
            <li v-else role="presentation" @click="toggleAside(false)">
              <router-link :to="item.path" role="button">
                {{item.label}}
              </router-link>
            </li>
          </template>
        </ul>
      </div>
    </div>
  </aside>
</template>

<script>
  import { bus, events } from './../bus'

  export default {
    components: {},
    props: ['isAsideShow'],
    data () {
      return {
        asideItems: [
          {
            label: 'Usage',
            items: [
              {path: '/getting-started', label: 'Getting Started'}
            ]
          },
          {
            label: 'Components',
            items: [
              {path: '/alert', label: 'Alert'},
              {path: '/carousel', label: 'Carousel'},
              {path: '/collapse', label: 'Collapse'},
              {path: '/date-picker', label: 'Date Picker'},
              {path: '/dropdown', label: 'Dropdown'},
              {path: '/modal', label: 'Modal'},
              {path: '/pagination', label: 'Pagination'},
              {path: '/popover', label: 'Popover'},
              {path: '/progress-bar', label: 'Progress Bar'},
              {path: '/tabs', label: 'Tabs'},
              {path: '/time-picker', label: 'Time Picker'},
              {path: '/tooltip', label: 'Tooltip'},
              {path: '/typeahead', label: 'Typeahead'}
            ]
          }
        ]
      }
    },
    methods: {
      toggleAside (show) {
        bus.$emit(events.TOGGLE_ASIDE, show)
      }
    }
  }
</script>

<style lang="less" rel="stylesheet/less" scoped>
  @import "./../../assets/css/variables";

  .search-box-placeholder-mixin {
    color: #CFD8DC;
    font-size: 12px
  }

  aside {
    position: fixed;
    left: 0;
    top: 0;
    width: @side-nav-width;
    height: 100vh;
    flex-shrink: 0;
    overflow-y: auto;
    overflow-x: hidden;
    z-index: 5;
    background: @aside-bg;
    box-shadow: 3px 0 6px rgba(0, 0, 0, 0.24);

    .brand {
      padding: 20px 15px;
      display: flex;
      flex-direction: column;
      align-items: center;
      border-bottom: 1px solid darken(@gray, 10%);

      .logo {
        height: 100px;
        width: 100%;
        position: relative;
        overflow: hidden;
        display: block;

        a {
          display: block;
          width: 100%;
          height: 100%;
        }

        .vue-logo {
          position: absolute;
          height: 100px;
          top: 0;
          left: 20%;
        }

        .bootstrap-logo {
          position: absolute;
          height: 60px;
          top: 20px;
          left: 50%;
          opacity: .8;
        }
      }
    }

    .nav-container {
      position: relative;

      .nav-div {
        position: relative;
      }

      .nav {
        li {
          margin: 0;

          a {
            color: #333;
            transition: all .3s ease-in-out;
            text-align: left;
            text-transform: none;
            padding: 15px 15px;
            border: 0;

            &.sub-list {
              padding: 10px 15px 10px 30px;
            }

            &.router-link-active {
              background: @side-nav-item-active-bg;
              color: @highlight-color;
              box-shadow: -6px 0 0 @highlight-color inset;
            }

            &:hover {
              background: @side-nav-item-active-bg;
            }
          }

          &.no-link {
            a {
              font-weight: bold;
              cursor: default;
              background: transparent;
            }
          }
        }
      }
    }
  }

  @media (max-width: @screen-xs-max) {
    aside {
      left: -275px;
      z-index: 1002;
      transition: left .3s ease-in-out;

      &.show {
        left: 0;
      }
    }
  }
</style>
