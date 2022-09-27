  <template>
  <div class="about">
    <div>
      <label>Results Per Page</label>
      <select v-model="fetch_limit" v-on:change="actionLimitChange">
        <option value="5">5</option>
        <option value="10">10</option>
        <option value="25">25</option>
        <option value="50">50</option>
        <option value="100">100</option>
        <option value="200">200</option>
      </select>
    </div>

    <div>
      <button v-on:click="paginatePrevious" :disabled="pagination.disable_previous">Previous</button>
      <button v-on:click="paginateNext" :disabled="pagination.disable_next">Next</button>
    </div>
    <table>
      <thead>
      <tr>
        <th>Image</th>
        <th>Title</th>
        <th></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="api_item in api_items">
        <td><img width="50" :src="api_item.thumbnailUrl" alt="{{api_item.title}}"></td>
        <td>{{ api_item.title }}</td>
        <td><a :href="api_item.url" target="_blank">View more</a></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
</style>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      api_items: [],
      fetch_start: 0,
      fetch_limit: 5,
      pagination: {
        'disable_previous': true,
        'disable_next': true
      }
    }
  },
  methods: {
    fetchApiItems(start, limit) {
      const view = this;
      axios.get('https://jsonplaceholder.typicode.com/photos?_start=' + start + '&_limit=' + limit).then(function (response) {
        view.api_items = response.data

        view.pagination.disable_previous = view.fetch_start < 1;
        view.pagination.disable_next = view.api_items.length < 1 && view.fetch_start > 0;
      }).catch(function (error) {
        console.log(error);
      })
    },
    actionLimitChange() {
      this.fetchApiItems(this.fetch_start, this.fetch_limit)
    },
    paginateNext() {
      this.fetch_start += parseInt(this.fetch_limit)
      this.fetchApiItems(this.fetch_start, this.fetch_limit)
    },
    paginatePrevious() {
      this.fetch_start -= parseInt(this.fetch_limit)
      this.fetchApiItems(this.fetch_start, this.fetch_limit)
    }

  },
  mounted() {
    this.fetchApiItems(this.fetch_start, this.fetch_limit)
  }
}
</script>
