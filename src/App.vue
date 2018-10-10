<template>
  <div class="container">
    <nav class="navbar">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="#"><img src="https://www.agentur-brandung.de/fileadmin/img/logo-250x74.png?1512470607" alt="brandung" /></a>
        </div>

        <form class="navbar-form navbar-right">
          <div class="form-group">
            <input type="text" class="form-control" placeholder="Search for..." name="query" v-model="searchQuery" />
            <span class="input-group-btn">
            </span>
          </div>
          <button class="btn btn-danger" type="button"
          @click="clearFilter()">Clear</button>
        </form>
      </div>
    </nav> 

    <div class="row">
      <div class="panel panel-info">
        <div class="panel-body">
          Telephone list
        </div>
        <div class="panel-footer">
          <demo-grid
            :data="gridData"
            :columns="gridColumns"
            :filter-key="searchQuery"
            @filterKey="searchQuery = $event">
          </demo-grid>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DemoGrid from './components/demo-grid';

export default {
  components: {
      'demo-grid': DemoGrid,
  },
  data: function() {
    return {
      searchQuery: '',
      gridColumns: ['firstName', 'surName', 'group', 'location', 'unit', 'dialing'],
      gridData: [
        { firstName: 'Adrian', surName: 'Gaspar', group: 'Office', location: 'Cologne', unit: 'Max', dialing: '126' },
        { firstName: 'Alexander', surName: 'Linn', group: 'Backend', location: 'Cologne', unit: 'brandung', dialing: '125' },
        { firstName: 'Alina', surName: 'Mühlenhoff', group: 'Projectmanagement', location: 'Cologne', unit: 'Max', dialing: '134' },
        { firstName: 'Alina', surName: 'Vollmer', group: 'Projectmanagement', location: 'Cologne', unit: 'Michael', dialing: '127' },
        { firstName: 'Alina', surName: 'Niemann', group: 'Creation', location: 'Berlin', unit: 'Niels', dialing: '136' },
        { firstName: 'Alois', surName: 'Rietzler', group: 'Backend', location: 'Berlin', unit: 'Niels', dialing: '122' },
        { firstName: 'Alwine', surName: 'Bannikow', group: 'Creation', location: 'Berlin', unit: 'Niels', dialing: '119' },
        { firstName: 'Andrea', surName: 'Löper', group: 'Creation', location: 'Berlin', unit: 'Niels', dialing: '123' },
        { firstName: 'Andreas', surName: 'Ewert', group: 'Projectmanagement', location: 'Cologne', unit: 'Max', dialing: '284' },
        { firstName: 'Andreas', surName: 'Bannikow', group: 'Frontend', location: 'Berlin', unit: 'Niels', dialing: '134' },
        { firstName: 'André', surName: 'Schober', group: 'Projectmanagement', location: 'Cologne', unit: 'Michael', dialing: '136' },
        { firstName: 'André', surName: 'Wenk', group: 'Backend', location: 'Berlin', unit: 'Niels', dialing: '116' },
        { firstName: 'Anja', surName: 'Meyer', group: 'Projectmanagement', location: 'Berlin', unit: 'Niels', dialing: '148' },
        { firstName: 'Backoffice', surName: 'Mirijam&Joyce', group: 'Office', location: 'Berlin', unit: 'brandung', dialing: '10' },
        { firstName: 'Benedict', surName: 'Plachta', group: 'Creation', location: 'Cologne', unit: 'Michael', dialing: '198' },
        { firstName: 'Björn', surName: 'Herzke', group: 'Backend', location: 'Berlin', unit: 'Niels', dialing: '118' },
        { firstName: 'Boris', surName: 'Funke', group: 'Backend', location: 'Cologne', unit: 'Max', dialing: '278' },
        { firstName: 'Boris', surName: 'Slogar', group: 'Backend', location: 'Cologne', unit: 'Max', dialing: '144' },
        { firstName: 'Christin', surName: 'Grunau', group: 'Frontend', location: 'Berlin', unit: 'Niels', dialing: '128' },
        { firstName: 'Christoph', surName: 'Franke', group: 'Backend', location: 'Berlin', unit: 'Niels', dialing: '129' },
        { firstName: 'Claire', surName: 'Serexhe', group: 'Projectmanagement', location: 'Cologne', unit: 'Max', dialing: '273' },
        { firstName: 'Daniel', surName: 'Steude', group: 'Projectmanagement', location: 'Cologne', unit: 'Max', dialing: '135' },
        { firstName: 'David', surName: 'Verholen', group: 'Backend', location: 'Cologne', unit: 'Max', dialing: '139' },
        { firstName: 'Demet', surName: 'Cinar', group: 'Creation', location: 'Cologne', unit: 'Max', dialing: '130' },
        { firstName: 'Denise', surName: 'Olbrich', group: 'Projectmanagement', location: 'Cologne', unit: 'Max', dialing: '149' },
        { firstName: 'Denise', surName: 'Kramm', group: 'Creation', location: 'Berlin', unit: 'Niels', dialing: '119' },
        { firstName: 'Dennis', surName: 'Busche', group: 'Backend', location: 'Cologne', unit: 'Michael', dialing: '163' },
        { firstName: 'Dorothea', surName: 'Buck', group: 'Frontend', location: 'Cologne', unit: 'Michael', dialing: '121' }
      ]
    }
  },
  methods: {
    clearFilter: function() {
      this.searchQuery = '';
    }
  }
}
</script>

<style lang="scss">
body {
  background-color: #b8d0de;
  color: #333;
  font-family: "Open Sans",Arial,sans-serif;
  line-height: 1.4;
}

.navbar {
  background-color: #fff;
}

.navbar-brand img {
  max-height: 100%;
}
</style>