<template>
  <div class="full-page-takeover-window">
    <div class="full-page-takeover-page">
      <Header
        :title="`Step ${activeStep} of ${stepsLength}`"
        exit-link="/instructor/course"
      />
      <div class="full-page-takeover-header-bottom-progress">
        <div
          :style="{width: progress}"
          class="full-page-takeover-header-bottom-progress-highlight"
        />
      </div>
      <div class="course-create full-page-takeover-container">
        <div class="container">
          <keep-alive>
            <component
              :is="activeComponent"
              ref="activeComponent"
              @stepUpdated="mergeFormData"
            />
          </keep-alive>
        </div>
        <div class="full-page-footer-row">
          <div class="container">
            <div class="full-page-footer-col">
              <div v-if="!isFirstStep">
                <a
                  class="button is-large"
                  @click.prevent="_previousStep"
                >Previous</a>
              </div>
              <div
                v-else
                class="empty-container"
              />
            </div>
            <div class="full-page-footer-col">
              <div>
                <button
                  v-if="!isLastStep"
                  :disabled="!canProceed"
                  class="button is-large float-right"
                  @click.prevent="_nextStep"
                >
                  Continue
                </button>
                <button
                  v-else
                  :disabled="!canProceed"
                  class="button is-success is-large float-right"
                  @click="createCourse"
                >
                  Confirm
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

import MultiComponentMixin from '@/mixins/MultiComponentMixin'

import Header from '~/components/shared/Header'
import CourseCreateStep1 from '~/components/instructor/CourseCreateStep1'
import CourseCreateStep2 from '~/components/instructor/CourseCreateStep2'

export default {
  layout: 'instructor',
  components: {
    Header,
    CourseCreateStep1,
    CourseCreateStep2
  },
  mixins: [MultiComponentMixin],
  fetch ({ store }) {
    return store.dispatch('category/fetchCategories')
  },
  data () {
    return {
      steps: ['CourseCreateStep1', 'CourseCreateStep2'],
      canProceed: false,
      form: {
        title: '',
        category: ''
      }
    }
  },
  computed: {
    ...mapState({
      categories: state => state.category.items
    })
  },
  methods: {
    _nextStep () {
      this.nextStep()
      this.$nextTick(() => (this.canProceed = this.$refs.activeComponent.isValid))
    },
    _previousStep () {
      this.previous()
      this.canProceed = true
    },
    mergeFormData ({ data, isValid }) {
      this.form = { ...this.form, ...data }
      this.canProceed = isValid
    },
    createCourse () {
      this.$store.dispatch('instructor/course/createCourse', this.form)
        .then(_ => this.$router.push('/instructor/courses'))
    }
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
