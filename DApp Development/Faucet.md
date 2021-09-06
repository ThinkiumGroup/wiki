<template>
  <div class="page-wrap">
    <div class="header">Thinkium test chain test coin faucet</div>
    <p>Automatically send 0.5 testnet TKM to your testnet address, you can get 5 testnet TKM at most</p>
    <p>The TKM here can only be used for testing</p>
    <p>Testnet TKM is issued to chain 1 by default</p>
    <div class="search-wrap">
      <div class="tab-wrap">
        <div class="tab-item" 
          v-for="(item, index) in tabList" 
          :key="index + item" 
          :class="{'active': selectedIndex === index}" 
        >
          {{item.label}}
        </div>
      </div>
      <div class="search" style="width:388px" v-show="selectedIndex == 1">
        <el-select v-model="coinAddressId" placeholder="please choose" style="width:100%">
          <el-option
            v-for="item in coinList"
            :key="item.id"
            :label="item.coinName"
            :value="item.id">
          </el-option>
        </el-select>
      </div>
      <div class="search">
        <el-input class="input" v-model="address" placeholder="Please enter your address..."></el-input>
        <div class="confirm-btn" @click="confirmBtn">Confirm</div>
      </div>
    </div>
  </div>
</template>

<script>
import { autoSendTestCoin, autoSendTRCCoin, getCoinAddress } from '../../../api/testNetwork.js';
import { isValidTHAddress, toAddress0x } from '../../../utils/common';
export default {
  data() {
    return {
      tabList: [
        {label: 'TKM', value: 1},
      ],
      selectedIndex: 0,
      address: '',
      amount: "",
      coinAddressId: '',
      coinList: []
    }
  },
  created() {
  },
  methods: {
    selectClick(index) {
      this.selectedIndex = index
      this.address = ""
    },
    async autoSendTestCoin() {
      let data = {
        toAddress: toAddress0x(this.address),
        type: this.tabList[this.selectedIndex].value
      }
      try{
          let res = await autoSendTestCoin(data);
          this.$message.success('Successfully issued')
      }catch(err){
         console.log('--err', err)
         this.$message.warning('The issuance fails or the address has already issued this type of test currency')
      }
      
    },
    confirmBtn() {
      this.address = this.address.trim();
      if(!this.address) {
        this.$message.warning('Please enter the address')
        return false
      }
      if(!isValidTHAddress(this.address)){
        this.$message.warning('Please enter the correct address')
        return
      }
      console.log(this.address)
      if(this.selectedIndex == 0) {
        this.autoSendTestCoin()
      }
      if(this.selectedIndex == 1) {
        this.autoSendTRCCoin()
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .page-wrap {
    padding-left: 26px;
    padding-top: 62px;
    .header {
      color: #212121;
      font-size: 24px;
      font-weight: bold;
      margin-bottom: 24px;
    }
    >p {
      color: #504F4F;
      font-size: 18px;
      line-height: 38px;
    }
    .search-wrap {
      background: #7139ff;
      width: 500px;
      padding: 30px 20px;
      margin-top: 30px;
      .tab-wrap {
        display: inline-flex;
        padding: 0 5px;
        background: #FFFFFF;
        border-radius: 4px;
        .tab-item {
          color: #C3AEF7;
          font-size: 20px;
          font-weight: 500;
          padding: 12px 15px;
          cursor: pointer;
          &.active {
            font-weight: bold;
            color: #7139ff;
            position: relative;
            &::after {
              display: inline-block;
              content: '';
              width: 24px;
              height: 3px;
              background: #7139ff;
              border-radius: 2px;
              position: absolute;
              bottom: 4px;
              left: calc(50% - 12px);
            }
          }
        }
      }
      .search {
        display: flex;
        width: 460px;
        height: 40px;
        background: #FFFFFF;
        border-radius: 4px;
        margin-top: 10px;
        .input {
          flex: 1;
        }
        .confirm-btn {
          width: 72px;
          height: 100%;
          display: flex;
          justify-content: center;
          align-items: center;
          color: #7139ff;
          font-size: 16px;
          line-height: 16px;
          font-weight: bold;
          border-left: 1px solid #D4C3FF;
          cursor: pointer;
        }
      }
    }
  }

</style>



