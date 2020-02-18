<template>
  <div>
    <hero />
    <section class="section">
      <div class="container">
        <h1 class="title">
          Featured Courses
        </h1>
        <div class="columns">
          <div
            v-for="course in courses"
            :key="course._id"
            class="column is-one-quarter"
          >
            <course-card :course="course" />
          </div>
        </div>
      </div>
    </section>
    <section
      class="
              section"
    >
      <div class="container">
        <h1 class="title">
          Featured Articles
        </h1>
        <div class="columns">
          <div class="column is-one-quarter">
            <blog-card />
          </div>
        </div>
      </div>
      </course-card>
    </section>
  </div>
  </div>
  </course-card>
  </div>
  </section>
  </div>
</template>

<script>
import { mapState } from 'vuex'

import CourseCard from '@/components/CourseCard'
import BlogCard from '@/components/BlogCard'
import Hero from '@/components/shared/Hero'

export default {
  components: {
    CourseCard,
    BlogCard,
    Hero
  },
  async fetch ({ store }) {
    await store.dispatch('course/fetchCourses')
  },
  computed: {
    ...mapState({
      courses: state => state.course.items
    })
  }
}
</script>

<style scoped lang="scss">
  // Home page
  .links {
    padding-top: 15px;
  }
</style>
