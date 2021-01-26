<template>
  <div>
    <div class="container">
      <h1 class="text-center">Escrow</h1>

      <div class="row">
        <div class="col-sm-12">
          <p>
            Balance: <b> {{ activeBalance }} </b> wei
          </p>
        </div>
      </div>

      <div class="row">
        <div class="col-sm-12">
          <form @submit.prevent="deposit">
            <div class="form-group">
              <label htmlFor="deposit">Deposit</label>
              <input
                type="number"
                v-model="amount"
                class="form-control"
                id="deposit"
              />
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
          </form>
        </div>
      </div>

      <br />

      <div class="row">
        <div class="col-sm-12">
          <button
            @click.prevent="release"
            type="submit"
            class="btn btn-primary"
          >
            Release
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  data: () => ({
    amount: 0,
  }),
  methods: {
    async deposit() {
      this.drizzleInstance.contracts.Escrow.methods.deposit().send({
        from: this.drizzleInstance.activeAccount,
        value: this.amount,
      });
    },
    async release() {
      this.drizzleInstance.contracts.Escrow.methods.release().send({
        from: this.drizzleInstance.activeAccount,
      });
    },
  },
  computed: {
    ...mapGetters("drizzle", ["drizzleInstance"]),
    ...mapGetters("accounts", ["activeBalance"]),
  },
};
</script>
