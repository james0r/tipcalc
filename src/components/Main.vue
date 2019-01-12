<template>
  <v-app>
    <v-container fluid>
      <div class="card">
        <v-text-field
          v-model="billtotal"
          :rules="billrules"
          label="Bill Total"
          required
          prefix="$"
 
        ></v-text-field>
        <v-select
          block
          :items="tipPercs"
          v-model="tipPerc"
          label="Tip Percentage"
          outline
          class="pt-3"
        ></v-select>
        <v-text-field
          v-model="partysize"
          class="party-size"
          :rules="partysizerules"
          label="Party Size (Split the bill by this many people)"
          required
        ></v-text-field>

        <v-btn @click="calc()" block color="info" style="margin-left: auto; float: right;">Calculate</v-btn>
        <v-btn @click="clear()" block color="success" style="margin-left: auto; float: right;">Reset</v-btn>
        <div class="tip-print-out">
          <h1 class="tip-label">Tip:</h1>
          <h1 :style="{color: tipColor}" class="tip-total">${{ tipPostCalc }}</h1>
        </div>
        <div class="total-print-out">
          <h1 class="total-label">Total:</h1>
          <h1 class="total-total">${{ totalPostCalc }}</h1>
        </div>
      </div>
    </v-container>
  </v-app>
</template>

<script>

export default {
  data() {
    return {
      billrules: [ v => !!v || 'Bill total is required!',
                  v => /^[1-9][\.\d]*(,\d+)?$/.test(v) || 'Bill must be numerical'],
      partysizerules: [ v => /^[0-9]+$/.test(v) || 'Party size must be an integer'],
      tipPercs: [10, 15, 17, 20],
      tipPerc: null,
      billtotal: null,
      partysize: null,
      totalPostCalc: 0.00,
      tipPostCalc: 0.00
    };
  },
  methods: {
    calc() {
      let total = parseFloat(this.billtotal) + (parseFloat(this.billtotal) * parseFloat(this.tipPerc / 100));
      this.totalPostCalc = total.toFixed(2);
      this.tipPostCalc = (parseFloat(this.billtotal) * parseFloat(this.tipPerc / 100)).toFixed(2);

      if (this.partysize !== null) {
        let tipSplit = (this.tipPostCalc / this.partysize);
        let totalSplit = (this.totalPostCalc / this.partysize);
        this.tipPostCalc = tipSplit.toFixed(2);
        this.totalPostCalc = totalSplit.toFixed(2);
      }
    },
    clear() {
      this.billtotal = null;
      this.tipPerc = null;
      this.totalPostCalc = 0.00;
      this.tipPostCalc = 0.00;
    }
  },
  computed: {
    tipColor() {
      if (this.tipPostCalc < 10.00) {
        return 'green'
      } else if (this.tipPostCalc < 20.00) {
        return 'yellow'
      } else if (this.tipPostCalc < 30.00) {
        return 'orange'
      } else if (this.tipPostCalc > 30.00) {
        return 'red'
      }
    }
  },
  components: {
    
  }

};
</script>

<style lang="scss" scoped>
.card {
  margin-left: auto;
  margin-right: auto;
  height: 80vh;
  max-width: 400px;
}

v-btn {
  float: right;
  margin-left: auto;
}

.tip-label {
  display: inline-block;
}

.tip-total {
  float: right;
}

.total-label {
  display: inline-block;
}

.total-total {
  float: right;
}
</style>


