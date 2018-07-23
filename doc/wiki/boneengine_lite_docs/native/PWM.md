## #PWM API


<div class="bi-table">
  <table>
    <colgroup>
      <col width="90px" />
      <col width="90px" />
    </colgroup>
    <tbody>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">API</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p">说明</div>
        </td>
      </tr>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">PWM.start(id)</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p"><span data-type="color" style="color:#F5222D">功能：</span>配置和启动PWM</div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">参数：</span> id:和板级配置文件中的id保持一致</div>
          <div data-type="p"> freq:频率</div>
          <div data-type="p"> duty:占空比</div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">返回值：</span>成功:返回资源handle,失败:-1</div>
        </td>
      </tr>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">PWM.getDuty(handle)</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p"><span data-type="color" style="color:#F5222D">功能：</span>获取当前pwm周期 </div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">参数：</span>handle:资源handle，为PWM.open的返回值; </div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">返回值：</span>占空比值
          </div>
        </td>
      </tr>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">PWM.setDuty(handle，duty)</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p"><span data-type="color" style="color:#F5222D">功能：</span>配置duty </div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">参数：</span> handle:资源handle，为PWM.open的返回值; </div>
          <div data-type="p"> duty:占空比值</div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">返回值：</span>0=ok other=fail
          </div>
        </td>
      </tr>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">PWM.getFreq(handle)</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p"><span data-type="color" style="color:#F5222D">功能：</span>获取当前pwm频率 </div>
          <div data-type="p">
            <span data-type="color" style="color:#F5222D">参数：</span>handle:资源handle，为PWM.open的返回值; </div>
          <div data-type="p">
            <span data-type="color" style="color:#F5222D">返回值：</span>频率值</div>
        </td>
      </tr>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">PWM.setFreq(handle, freq)</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p"><span data-type="color" style="color:#F5222D">功能：</span>配置freq </div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">参数：</span> handle:资源handle，为PWM.open的返回值;</div>
          <div data-type="p"> freq:频率 </div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">返回值：</span>0=ok other=fail
          </div>
        </td>
      </tr>
      <tr height="34px">
        <td rowspan="1" colSpan="1">
          <div data-type="p">PWM.stop(handle)</div>
        </td>
        <td rowspan="1" colSpan="1">
          <div data-type="p"><span data-type="color" style="color:#F5222D">功能：</span>停止PWM </div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">参数：</span> handle:资源handle，为PWM.open的返回值;</div>
          <div data-type="p"><span data-type="color" style="color:#F5222D">返回值：</span>0=ok other=fail
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</div>


## #板级配置参数


<div class="bi-table">

## #板级配置示范
```json
{
	"PWM":[
		{
		"id":"buzzer",
		"port":4,
		"freq":5000,
		"duty":50
		}
	]
}
```


## #ESP32之无源蜂鸣器
### #硬件


![1jpg.png | left | 423x409](https://cdn.yuque.com/lark/0/2018/png/66207/1525852711659-02a89502-721f-462a-b7e7-3c00022c67b0.png "")


### #接线
EPS32 IO4引脚 连接 无源蜂鸣器模块的'+'引脚；
EPS32 GND引脚 连接 无源蜂鸣器模块的GND引脚；
### #配置
```json
/*apps/js/board_config.json*/
{
	"PWM":[
		{
		"id":"buzzer",
		"port":4,
		"freq":5000,
		"duty":50
		}
	]

}
```

### #代码
```javascript
/*samples/js/buzzer.js*/
print('buzzer uart test.....................');
var buzzer_handle=PWM.start('buzzer'); 
var cur_duty = PWM.getDuty(buzzer_handle);
console.log('cur_duty:'+cur_duty);
setInterval(function() {
	cur_duty += 1;
	if(cur_duty >= 100)cur_duty=0;
	PWM.setDuty(buzzer_handle,cur_duty);
}, 500);
print('end buzzer test........................');
```

### #现象
蜂鸣器声音由弱到强转换。
## #TODO


 