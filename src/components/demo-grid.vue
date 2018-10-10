<template>
  <table class="table table-hover">
    <thead>
      <tr>
        <th>#</th>
        <th v-for="key in columns"
          @click="sortBy(key)"
          :class="{ active: sortKey == key }">
          {{ key | capitalize }}
          <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(entry, index) in filteredData"
        :class="{ success: entry['group'] === 'Frontend',
                  warning: entry['group'] === 'Backend',
                  info: entry['group'] === 'Projectmanagement',
                  danger: entry['group'] === 'Creation' }">
        <td>{{ index + 1 }}</td>
        <td v-for="key in columns">
          <template v-if="key === 'dialing'">
            <a :href="getTelephone(entry['location'], entry[key])" class="btn btn-primary btn-sm">
                <span class="glyphicon glyphicon-earphone" aria-hidden="true">
                    {{ entry[key] }}
                </span> 
            </a>
          </template>
          <template v-else-if="key === 'group'">
            <span class="label"
            :class="{ 'label-success': entry['group'] === 'Frontend',
                      'label-warning': entry['group'] === 'Backend',
                      'label-info': entry['group'] === 'Projectmanagement',
                      'label-danger': entry['group'] === 'Creation',
                      'label-default': entry['group'] === 'Office' || entry['group'] === 'Brandung' }"
            @click="changeData(entry[key])">{{ entry[key] }}</span>
          </template>
          <template v-else-if="key === 'location' || key === 'unit'">
            <span class="label label-default"
            @click="changeData(entry[key])">{{ entry[key] }}</span>
          </template>
          <template v-else>
            {{ entry[key] }}
          </template>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
    props: {
        data: Array,
        columns: Array,
        filterKey: String
    }, 
    data: function () {
        var sortOrders = {};
        this.columns.forEach(function (key) {
            sortOrders[key] = 1;
        })
        return {
            sortKey: '',
            sortOrders: sortOrders
        }
    },
    computed: {
        filteredData: function () {
            var sortKey = this.sortKey;
            var filterKey = this.filterKey && this.filterKey.toLowerCase();
            var order = this.sortOrders[sortKey] || 1;
            var data = this.data;
            if (filterKey) {
                data = data.filter(function (row) {
                    return Object.keys(row).some(function (key) {
                        return String(row[key]).toLowerCase().indexOf(filterKey) > -1;
                    })
                })
            }
            if (sortKey) {
                data = data.slice().sort(function (a, b) {
                    a = a[sortKey];
                    b = b[sortKey];
                    return (a === b ? 0 : a > b ? 1 : -1) * order;
                })
            }
            return data;
        }
    },
    filters: {
        capitalize: function (str) {
            return str.charAt(0).toUpperCase() + str.slice(1);
        }
    },
    methods: {
        sortBy: function (key) {
            this.sortKey = key;
            this.sortOrders[key] = this.sortOrders[key] * -1;
        },
        changeData: function (key) {
            this.filterKey = key;
            this.$emit("filterKey", this.filterKey);
        },
        getTelephone: function(location, dialing) {
            if (location === 'Cologne') {
                return 'tel:0221913920' + dialing;
            } else {
                return 'tel:0306167146' + dialing;
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #000;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #000;
}

.label:hover {
  cursor: pointer;
}
</style>