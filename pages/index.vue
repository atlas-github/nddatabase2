<template>
  <div class="bg-cover bg-gray-100 font-roboto">
    <div
      class="max-w-3xl max-w-5xl min-h-screen flex justify-center mx-auto py-5"
    >
      <main class="w-full">
        <div class="bg-[#479900] bg-cover p-1 rounded-lg text-white">
          <h1 class="text-2xl font-semibold m-1">Nominee Director Database</h1>
        </div>
        <div>
          <section>
            <form class="flex flex-col space-y-2" autocomplete="off">
              <input
                id="search-blogs"
                v-model="query"
                class="px-3 py-2 shadow border border-gray-200 my-3 rounded-lg"
                type="text"
                placeholder="corporate management [male] malay"
              />
            </form>
          </section>
          <!-- buttons are not working yet -->
          <div v-if="false">
            <section class="mb-3 ml-2">
              <button
                type="button"
                class="
                  bg-gray-500
                  rounded-full
                  text-white
                  font-semibold
                  py-1
                  px-4
                  mx-1
                  hover:bg-[#312D8F]
                "
              >
                All
              </button>
              <button
                type="button"
                class="
                  bg-gray-500
                  rounded-full
                  text-white
                  font-semibold
                  py-1
                  px-4
                  mx-1
                  hover:bg-[#312D8F]
                "
              >
                Male
              </button>
              <button
                type="button"
                class="
                  bg-gray-500
                  rounded-full
                  text-white
                  font-semibold
                  py-1
                  px-4
                  mx-1
                  hover:bg-[#312D8F]
                "
              >
                Female
              </button>
            </section>
          </div>
          <section class="space-y-4">
            <article
              v-for="post of posts"
              :key="post.slug"
              class="hover:scale-[1.03] rounded-lg p-2 bg-cover bg-white"
            >
              <div class="flex items-center flex-wrap mb-2">
                <img
                  :src="post.profile_pic"
                  class="h-14 w-14 rounded-full mr-2"
                  alt=""
                />
                <div class="grid grid-rows-2">
                  <h2
                    class="
                      text-lg text-blue-700
                      hover:text-blue-800
                      font-semibold
                    "
                  >
                    <a
                      :href="post.slug"
                      target="_blank"
                      class="hover:underline"
                    >
                      {{ post.title }}
                    </a>
                  </h2>
                  <p class="text-sm">{{ post.education }}</p>
                </div>
              </div>
              <span>
                <p class="ml-1 mb-1 font-semibold">
                  Current position(s):
                  {{ post.current_position }}
                </p>
                <p class="ml-1 mb-1">
                  Previous position(s):
                  {{ post.previous_position }}
                </p>
                <p class="ml-1 mb-1 font-semibold">
                  Comment:
                  {{ post.comment }}
                </p>
              </span>
              <div class="my-2 flex justify-start">
                <p
                  class="
                    bg-[#479900]
                    rounded-full
                    text-white
                    font-semibold
                    py-1
                    px-4
                    mx-1
                  "
                >
                  {{ post.skillset1 }}
                </p>
                <p
                  class="
                    bg-[#479900]
                    rounded-full
                    text-white
                    font-semibold
                    py-1
                    px-4
                    mx-1
                  "
                >
                  {{ post.skillset2 }}
                </p>
                <p
                  class="
                    bg-[#479900]
                    rounded-full
                    text-white
                    font-semibold
                    py-1
                    px-4
                    mx-1
                  "
                >
                  {{ post.skillset3 }}
                </p>
              </div>
            </article>
          </section>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: '',
      posts: [],
    }
  },
  async fetch() {
    if (!this.query) {
      this.posts = await this.$content().fetch()
      return
    }
    this.posts = await this.$content().search(this.query).fetch()
  },
  watch: {
    query: '$fetch',
  },
}
</script>
