<template>
  <div class="mod-home">
    <!-- 主标题与引言 -->
    <h1>“好周到”商城系统管理后台欢迎您</h1>
    <p class="subtitle">
      这里是商城运营的<strong>智能中枢</strong>，为您提供 <strong>全流程数字化管理方案</strong>，
      让商城运营更高效、更精准、更省心。
    </p>

    <!-- 核心功能模块 -->
    <h2>一、核心功能：覆盖运营全场景</h2>
    <p>我们围绕「人、货、场」构建核心能力，让管理更简单：</p>
    <ul class="feature-list">
      <li>
        <strong>商品管理</strong>：批量操作（上架/下架/改价）、多规格配置、库存预警，快速搭建丰富商品矩阵；
      </li>
      <li>
        <strong>订单处理</strong>：实时追踪状态（待付款/发货/售后），物流无缝同步，纠纷高效闭环；
      </li>
      <li>
        <strong>用户运营</strong>：会员分层、精准营销（优惠券/满减/弹窗），私域流量深度激活；
      </li>
      <li>
        <strong>数据洞察</strong>：可视化看板（订单趋势、访客画像、热销榜单），用数据替代「拍脑袋」决策。
      </li>
    </ul>

    <!-- 实时看板模块 -->
    <h2>二、实时看板：一眼掌握运营动态</h2>
    <p>首页集成 <strong>「今日关键数据」</strong> 看板：</p>
    <ul class="dashboard-list">
      <li>实时更新：今日订单量、访客数、客单价；</li>
      <li>重点预警：库存告急商品、退单激增风险、新客来源变化；</li>
      <li>趋势预判：基于历史数据，智能预测明日销量、流量峰值。</li>
    </ul>

    <!-- 服务保障模块 -->
    <h2>三、服务保障：让您“无后顾之忧”</h2>
    <ul class="service-list">
      <li>
        🔹 <strong>持续进化</strong>：系统定期更新功能（如直播带货、社群营销模块持续拓展），紧跟行业趋势；
      </li>
      <li>
        🔹 <strong>专属支持</strong>：7×12小时客服响应，操作手册、故障排查一键直达，小白也能快速上手；
      </li>
      <li>
        🔹 <strong>安全兜底</strong>：数据加密存储、多角色权限管控，保障商城交易稳定、用户信息安全。
      </li>
    </ul>

    <!-- 收尾总结 -->
    <p class="conclusion">
      从「商品上架」到「用户复购」，从「数据监控」到「风险预警」——
      <strong>“好周到”以「全链路服务」理念，陪您的商城“稳稳成长”</strong>。
    </p>
    <p class="call-to-action">现在，就从这里开启 <strong>“高效运营”之旅</strong> 吧！</p>
  </div>
</template>

<style lang="scss" scoped>
.mod-home {
  line-height: 1.6;
  padding: 24px;
  color: #333;

  /* 主标题 */
  h1 {
    font-size: 24px;
    font-weight: 600;
    margin-bottom: 12px;
    color: #2f4050;
  }

  /* 副标题 */
  .subtitle {
    font-size: 16px;
    color: #666;
    margin-bottom: 24px;
  }

  /* 二级标题 */
  h2 {
    font-size: 20px;
    font-weight: 600;
    margin: 32px 0 16px;
    color: #1f2d3d;
    position: relative;
    padding-left: 12px;

    &::before {
      content: "";
      position: absolute;
      left: 0;
      top: 6px;
      width: 4px;
      height: 16px;
      background: #4898d5; /* 蓝色标识增强层次感 */
    }
  }

  /* 段落通用 */
  p {
    margin-bottom: 12px;
  }

  /* 功能列表（自定义圆点） */
  .feature-list, .service-list {
    list-style: none;
    padding-left: 16px;
    margin-bottom: 20px;

    li {
      margin-bottom: 8px;
      &::before {
        content: "•";
        color: #4898d5;
        margin-right: 6px;
      }
    }
  }

  /* 看板列表（默认圆点） */
  .dashboard-list {
    list-style: disc;
    padding-left: 24px;
    color: #555;
    margin-bottom: 20px;

    li {
      margin-bottom: 6px;
    }
  }

  /* 总结文案 */
  .conclusion {
    font-weight: 500;
    color: #2f4050;
    margin: 24px 0;
  }

  /* 行动引导 */
  .call-to-action {
    font-size: 16px;
    font-weight: 600;
    color: #ff6600; /* 橙色强调 */
  }

  /* 强调文本统一配色 */
  strong {
    color: #ff6600;
  }
}
</style>
