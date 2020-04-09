<template>
    <div class="row">
      <div class="col-lg-12 col-md-12">
        <div class="card">
          <h4 slot="header" class="card-title"></h4>
          <div class="chart-area">
            <ClusteredBar></ClusteredBar>
          </div>
        </div>
      </div>
    </div>
</template>
<script>
 import ClusteredBar from 'components/Dashboard/ClusteredBar'
export default {
  components: {
      ClusteredBar
  },
};
</script>