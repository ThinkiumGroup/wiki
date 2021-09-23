<template>
  <div class="page-wrap">
    <div class="header">{{lan('testCoinFaucet')}}</div>
    <p>{{lan('automaticallySendTestnet')}}</p>
    <p>{{lan('onlyBeUsedForTesting')}}</p>
    <p>{{lan('chain1ByDefault')}}</p>
    <div class="search-wrap">
      <div class="search" style="width:388px" v-show="selectedIndex == 1">
        <el-select v-model="coinAddressId" :placeholder="lan('pleaseChoose')" style="width:100%">
          <el-option
            v-for="item in coinList"
            :key="item.id"
            :label="item.coinName"
            :value="item.id">
          </el-option>
        </el-select>
      </div>
      <div class="search">
        <el-input class="input" v-model="address" :placeholder="lan('enterYourAddress')" @change="onInputChange"></el-input>
        <div class="confirm-btn" @click="confirmBtn">{{lan('receive')}}</div>
        <div class="confirm-btn" style="width: 150px" @click="checkAccount">{{lan('checkBalance')}}</div>
      </div>
      <div class="account" v-show="currentAccountVaule">
        {{lan('currentAccountBalance') + currentAccountVaule}}
      </div>
    </div>
  </div>
</template>

<script>
import { autoSendTestCoin, autoSendTRCCoin, getCoinAddress, getAccount } from '../../api/testNetwork.js';
import { isValidTHAddress, isValid0xAddress, toAddress0x } from '../../utils/common';
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
      coinList: [],
      currentAccountVaule: 0,
    }
  },
  created() {
  },
  methods: {
    onInputChange(){
      this.currentAccountVaule = 0;
    },
    selectClick(index) {
      this.selectedIndex = index
      this.address = ""
    },
    async autoSendTestCoin() {
      let data = {
        toAddress: isValid0xAddress(this.address)? this.address.toLowerCase() : toAddress0x(this.address),
        type: this.tabList[this.selectedIndex].value
      }
     autoSendTestCoin(data).then((res) => {
        if(res.code == 200){
          this.$message.success(this.lan('successfullyIssued'))
        }else if(res.code == 2000){
          this.$message.warning(this.lan('alreadyAppliedToday'))
        }else{
          this.$message.warning(this.lan('issuanceFailed'))
        };
     })
    },
    checkInput(){
      this.address = this.address.trim();
      if(!this.address) {
        this.$message.warning(this.lan('enterTheAddress'))
        return false
      }
      if(!isValidTHAddress(this.address) && !isValid0xAddress(this.address)){
        this.$message.warning(this.lan('enterTheCorrectAddress'))
        return false
      }
      return true;
    },
    checkAccount(){
      if(!this.checkInput()){
        return;
      }
       const loading = this.$loading({
          lock: true,
          text: 'Loading',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
      let data = {
        chainId: '1',
        address: isValid0xAddress(this.address)? this.address.toLowerCase() : toAddress0x(this.address)
      }
      getAccount(data).then((res) => {
        if(res.code == 200){
          let data = res['data'] || {};
          this.currentAccountVaule = data.balanceValue;
        }
        loading.close();
      }).catch((err) => {
        console.log('--err')
        loading.close();
      })
    },
    confirmBtn() {
      if(!this.checkInput()){
        return;
      }
      console.log(this.address)
      if(this.selectedIndex == 0) {
        this.autoSendTestCoin()
      }
      if(this.selectedIndex == 1) {
        this.autoSendTRCCoin()
      }
    },
    lan(key){
      return this.$lan && this.$lan.en[key] || '';
    }
  },
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
      .account{
        color: #FFF;
        margin-top: 10px;
        font-weight: 500;
      }
    }
  }

  /deep/.el-input__inner{
    border: none !important;
  }

</style>

