<template>
    <div>
        <card class="flex flex-col">
          <h1 v-if="title" class="py-6 text-90 font-normal text-2xl text-left pl-4">{{ title }}</h1>
          <table cellpadding="0" cellspacing="0" data-testid="resource-table" class="table w-full">
            <thead>
              <tr>
                <th class="text-left" v-for="head in header">
                  <span class="cursor-pointer inline-flex items-center">
                    {{ head }}
                  </span>
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="row in data">
                <td v-for="column in row.columns" v-html="column"></td>
                <td class="td-fit text-right pr-6">
                  <span v-if="row.view">
                    <router-link
                        class="cursor-pointer text-70 hover:text-primary mr-3"
                        :to="row.view"
                        :title="__('View')"
                    >
                    <icon type="view" width="22" height="18" view-box="0 0 22 16" />
                  </router-link>
                  </span>
                </td>
              </tr>
            </tbody>
          </table>
        </card>
    </div>
</template>

<script>
export default {
    props: ['card'],

    data() {
      return {
        data: [],
        header: [],
        title: '',
      }
    },

    async mounted() {
        const { data } = await Nova.request().get('/nova-vendor/customtablecard/')
        this.data = data.data
        this.header = data.header
        this.title = data.title

      console.log(this.data)
    },
}
</script>
