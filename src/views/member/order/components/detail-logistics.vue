<template>
    <div class="detail-logistics">
        <p>
            <span>{{list[0].text}}</span>
            <span>{{list[0].time}}</span>
        </p>
        <a href="javascript:;" @click="handlerLogistics(order)">查看物流</a>
        <Teleport to="#model">
        <OrderLogistics ref="orderLogisticsCom" />
      </Teleport>
    </div>
</template>
<script>
import OrderLogistics from './order-logistics.vue'
import { logisticsOrder } from '@/api/order'
import { useLogistics } from '../index.vue'
import { ref } from 'vue'
export default {
  name: 'DetailLogistics',
  props: {
    order: {
      type: Object,
      default: () => ({})
    }
  },
  components: { OrderLogistics },
  async setup (props) {
    const data = await logisticsOrder(props.order.id)
    const list = ref(data.result.list)
    return { list, ...useLogistics() }
  }
}
</script>
<style scoped lang="less">
.detail-logistics {
    height: 50px;
    display: flex;
    align-items: center;
    padding: 0 30px;
    background-color: #f5f5f5;
    margin: 30px 50px 0;

    >p {
        flex: 1;

        span {
            color: #999;

            &:first-child {
                margin-right: 30px;
            }
        }
    }

    >a {
        color: @xtxColor;
        text-align: center;
    }
}
</style>
