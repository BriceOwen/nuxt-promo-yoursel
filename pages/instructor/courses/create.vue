<template>
  <div class="full-page-takeover-window">
    <div class="full-page-takeover-page">
      <Header
        :title="`Step 1 of 2`"
        exit-link="#"
      />
      <div class="full-page-takeover-header-bottom-progress">
        <div
          :style="{width: '50%'}"
          class="full-page-takeover-header-bottom-progress-highlight"
        />
      </div>
      <div class="course-create full-page-takeover-container">
        <div class="container">
          <CourseCreateStep1 />
          <CourseCreateStep2 />
        </div>
        <div class="full-page-footer-row">
          <div class="container">
            <div class="full-page-footer-col">
              <div>
                <a
                  class="button is-large"
                  @click.prevent="() => {}"
                >Previous</a>
              </div>
              <!-- <div v-else class="empty-container">
              </div> -->
            </div>
            <div class="full-page-footer-col">
              <div>
                <button
                  class="button is-large float-right"
                  @click.prevent="() => {}"
                >
                  Continue
                </button>
                <!-- <button
                  @click="() => {}"
                  class="button is-success is-large float-right">
                  Confirm
                </button> -->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '~/components/shared/Header'
import CourseCreateStep1 from '~/components/instructor/CourseCreateStep1'
import CourseCreateStep2 from '~/components/instructor/CourseCreateStep2'
export default {
  layout: 'instructor',
  components: {
    Header,
    CourseCreateStep1,
    CourseCreateStep2
  }
}
</script>

<style lang="scss">
  .float-right {
    float: right;
  }
  .empty-container {
    width: 1px;
    height: 1px;
  }
  .course-create {
    &-wrapper {
      margin-top: 60px;
      text-align: center;
    }
    &-headerText {
      font-weight: 500;
      line-height: 1.1;
      margin-top: 21px;
      margin-bottom: 10.5px;
      font-size: 36px;
      font-weight: 300;
    }
    &-subtitle {
      font-size: 24px;
      font-weight: 300;
      margin-top: 21px;
      margin-bottom: 10.5px;
    }
    &-form {
      margin-top: 60px;
      &-group {
        display: flex;
        flex-direction: column;
        align-items: center;
      }
      &-field {
        min-width: 552px;
      }
      .select {
        width: 100%;
        >select {
          width: 100%;
        }
      }
    }
  }
</style>