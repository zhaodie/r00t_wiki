---
home: true
heroImage: /img/home.svg
actionBtn:
  text: å¼å§ä½¿ç¨ð
  link: /about/
  type: primary
  ghost: true
  size: large
preactionBtn:
  text: æ¯æé¡¹ç®ð
  link: /about/support
  type: primary
  ghost: true
  size: large
features:
- title: å®ç¨
  details: æ¶å½äºèç½ä¸­åç±»æç« 
- title: è¯¦ç»
  details: å¨é¢çä¿®å¤åéªè¯æ¹æ³
- title: å¼æº
  details: æ¯ä¸ªäººé½å¯ä»¥èªç±æ­å»º

head: [
    ['link', { rel: 'icon', href: '/img/home.svg' }],
    ['meta', { name: 'referrer', content: 'never' }],
    ['meta', { name: 'keywords', content: 'ç¥è¯åº,æ¼æ´å¤ç°,r00tæåº,ä»£ç å®¡è®¡,æ¸éæµè¯' }],
    ['meta', { name: 'description', content: 'å¦ä»æ¼æ´çåç§å¤ç°æç« å·²ç»å¡«æ»¡äºäºèç½ï¼ä½æ¯æ¯æ¬¡å»å°è¯æ¼æ´å¤ç°æ¶ï¼æ»ä¼çº ç»äºç¯å¢æ­å»ºï¼POCåæ¼æ´åçä¸ãç±äºè¿äºå ç´ ï¼éå¸¸é½éè¦ç¿»éå¾å¤å¾å¤çæç« æè½çè§£è¿ä¸ªæ¼æ´ï¼äºæ¯ï¼ä¾¿èçäºæç¯å¢æ­å»ºï¼POCï¼æ¼æ´åçå¨é¨éåå¨ä¸ä¸ªæåºçæ³æ³ï¼r00t WiKi-POCæåºä¾¿ç±æ­¤èæ¥ð£' }],
  ]
footer: Powered by r00tæåº | Copyright Â© 2021-2022 r00tæåº
---

</br>
</br>
<a-alert type="info" message="æç¤º" description="ç±äºä¼ æ­ãå©ç¨æ­¤æææä¾çä¿¡æ¯èé æçä»»ä½ç´æ¥æèé´æ¥çåæåæå¤±ï¼åç±ä½¿ç¨èæ¬äººè´è´£ï¼æç« ä½èä¸ä¸ºæ­¤æ¿æä»»ä½è´£ä»»ãr00tæåº æ¥æå¯¹æ­¤æç« çä¿®æ¹åè§£éæå¦æ¬²è½¬è½½æä¼ æ­æ­¤æç« ï¼å¿é¡»ä¿è¯æ­¤æç« çå®æ´æ§ï¼åæ¬çæå£°æç­å¨é¨åå®¹ãæªç»ä½èåè®¸ï¼ä¸å¾ä»»æä¿®æ¹æèå¢åæ­¤æç« åå®¹ï¼ä¸å¾ä»¥ä»»ä½æ¹å¼å°å¶ç¨äºåä¸ç®çã" showIcon>
</a-alert>

</br>
</br>

<template>
  <a-steps>
    <a-step status="finish" title="Login Github">
      <a-icon slot="icon" type="github" />
    </a-step>
    <a-step status="finish" title="Star">
      <a-icon slot="icon" type="star" />
    </a-step>
    <a-step status="process" title="Reading">
      <a-icon slot="icon" type="loading" />
    </a-step>
    <a-step status="wait" title="Thank">
      <a-icon slot="icon" type="smile-o" />
    </a-step>
  </a-steps>
</template>