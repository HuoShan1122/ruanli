<template>
  <div>
    <el-card>
      <el-form ref="form" :model="form" label-width="80px">
        <el-row>
          <el-col :span="12">
            <el-form-item label="省">
              <el-select v-model="form.region" placeholder="请选择省">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="市">
              <el-select v-model="form.region" placeholder="请选择市">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="县">
              <el-select v-model="form.region" placeholder="请选择县">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="乡镇">
              <el-select v-model="form.region" placeholder="请选择乡镇">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="村">
          <el-select v-model="form.region" placeholder="请选择村">
            <el-option label="区域一" value="shanghai"></el-option>
            <el-option label="区域二" value="beijing"></el-option>
          </el-select>
        </el-form-item>

        <el-form-item label="时间">
          <el-date-picker
            v-model="form.time"
            type="datetime"
            placeholder="选择日期时间"
          ></el-date-picker>
        </el-form-item>

        <el-form
          :model="ruleForm"
          :rules="rules"
          ref="ruleForm"
          label-width="80px"
          class="demo-ruleForm"
        >
          <el-form-item label="来源" prop="source">
            <el-cascader
              v-model="ruleForm.source"
              :options="options1"
              @change="handleChange"
            ></el-cascader>
          </el-form-item>

          <el-form-item label="载体" prop="carrier">
            <el-select v-model="ruleForm.carrier" placeholder="请选择">
              <el-option
                v-for="item in options2"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              ></el-option>
            </el-select>
          </el-form-item>

          <el-form-item label="灾情" prop="damageSituation">
            <el-cascader
              v-model="ruleForm.damageSituation"
              :options="options3"
              @change="handleChange"
            ></el-cascader>
          </el-form-item>

          <el-form-item label="灾情描述" prop="description">
            <el-input type="textarea" v-model="ruleForm.description"></el-input>
          </el-form-item>
        </el-form>

        <el-form-item label="上传文件">
          <el-upload
            class="upload-demo"
            drag
            action="https://jsonplaceholder.typicode.com/posts/"
            multiple
          >
            <i class="el-icon-upload"></i>
            <div class="el-upload__text">
              将文件拖到此处，或<em>点击上传</em>
            </div>
            <div class="el-upload__tip" slot="tip">
              只能上传jpg/png文件，且不超过500kb
            </div>
          </el-upload>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')"
            >提交</el-button
          >
          <el-button @click="resetForm('ruleForm')">重置</el-button>
        </el-form-item>
      </el-form>
    </el-card>

    <el-card>
      <h2>1.用户名</h2>
      用户登录后系统将会自动填写用户名。
      <h2>2.行政区划</h2>
      行政区划存在固定格式，请根据国家统计局所给出的标准进行填写。地址如下：
      国家统计局行政区划
      <h2>3.时间</h2>
      请在弹出的时间选择框中选择灾情发生的时间，可以点击右下角的“此刻”来自动生成此时的时间字符串。
      <h2>4.来源、载体、灾情</h2>
      点击级联选择框选择
      <h2>5.描述</h2>
      在文本输入框中输入信息
      <h2>6.上传文件</h2>
      拖拽或点击上传文件，文件大小格式数量均无限制
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        region: "",
        date1: "",
        date2: "",
        time: "",
        // source: [], //来源
        // carrier: "", //载体
        // damageSituation: "", //灾情
      },
      ruleForm: {
        source: "",
        carrier: "",
        damageSituation: "",
        description: "",
      },
      rules: {
        source: [{ required: true, message: "请输入来源", trigger: "change" }],
        carrier: [{ required: true, message: "请输入载体", trigger: "change" }],
        damageSituation: [
          { required: true, message: "请输入灾情", trigger: "change" },
        ],
        description: [
          { required: true, message: "请输入灾情描述", trigger: "blur" },
        ],
      },

      options1: [
        {
          value: "guanfangbaosongshuju",
          label: "官方报送数据",
          children: [
            {
              value: "qianfangdizhenyongjizhihuibu",
              label: "前方地震应急指挥部",
            },
            {
              value: "houfangdizhenyingjizhihuibu",
              label: "后方地震应急指挥部",
            },
            {
              value: "zhihuihekongzhizhongxin",
              label: "指挥和控制中心",
            },
            {
              value: "shehuifuwugongchengyingjijiuyuanxitong",
              label: "社会服务工程应急救援系统",
            },
            {
              value: "dangdidizhenju",
              label: "当地地震局",
            },
            {
              value: "guojiadizhenju",
              label: "国家地震局",
            },
            {
              value: "yingjixinxifuwujishuxitong",
              label: "应急信息服务技术系统",
            },
            {
              value: "qita",
              label: "其他",
            },
          ],
        },
        {
          value: "zuwangganzhishuju",
          label: "组网感知数据",
          children: [
            {
              value: "tongxinwangganzhi",
              label: "通信网感知",
            },
            {
              value: "dianlixitongganzhi",
              label: "电力系统感知",
            },
            {
              value: "jiaotongxitongganzhi",
              label: "交通系统感知",
            },
            {
              value: "tianyanxitongganzhi",
              label: "天眼系统感知",
            },
            {
              value: "qita",
              label: "其他",
            },
          ],
        },
        {
          value: "qitashuju",
          label: "其他数据",
          children: [
            {
              value: "qitashuju",
              label: "其他数据",
            },
          ],
        },
      ],

      options2: [
        {
          value: "text",
          label: "文字",
        },
        {
          value: "image",
          label: "图像",
        },
        {
          value: "audio",
          label: "音频",
        },
        {
          value: "video",
          label: "视频",
        },
        {
          value: "others",
          label: "其他",
        },
      ],

      options3: [
        {
          value: "earthquakeSituation",
          label: "震情",
          children: [
            {
              value: "earthquakeSituationInfo",
              label: "震情信息",
              children: [
                {
                  value: "location",
                  label: "地理位置",
                },
                {
                  value: "time",
                  label: "时间",
                },
                {
                  value: "magnititude",
                  label: "震级",
                },
                {
                  value: "depth",
                  label: "震源深度",
                },
                {
                  value: "intensity",
                  label: "烈度",
                },
              ],
            },
          ],
        },
        {
          value: "casualties",
          label: "人员伤亡及失踪",
          children: [
            {
              value: "death",
              label: "死亡",
              children: [
                {
                  value: "number",
                  label: "受灾人数",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "hurt",
              label: "受伤",
              children: [
                {
                  value: "number",
                  label: "受灾人数",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "missing",
              label: "失踪",
              children: [
                {
                  value: "number",
                  label: "受灾人数",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
          ],
        },
        {
          value: "buildingDamage",
          label: "房屋破坏",
          children: [
            {
              value: "tumu",
              label: "土木",
              children: [
                {
                  value: "normal",
                  label: "一般损坏面积",
                },
                {
                  value: "serious",
                  label: "严重损坏面积",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "zhuanmu",
              label: "砖木",
              children: [
                {
                  value: "normal",
                  label: "一般损坏面积",
                },
                {
                  value: "serious",
                  label: "严重损坏面积",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "zhuanhun",
              label: "砖混",
              children: [
                {
                  value: "normal",
                  label: "一般损坏面积",
                },
                {
                  value: "serious",
                  label: "严重损坏面积",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "kuangjia",
              label: "框架",
              children: [
                {
                  value: "normal",
                  label: "一般损坏面积",
                },
                {
                  value: "serious",
                  label: "严重损坏面积",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "qita",
              label: "其他",
              children: [
                {
                  value: "normal",
                  label: "一般损坏面积",
                },
                {
                  value: "serious",
                  label: "严重损坏面积",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
          ],
        },
        {
          value: "lifeLine",
          label: "生命线灾情工程",
          children: [
            {
              value: "traffic",
              label: "交通",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "water",
              label: "供水",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "oil",
              label: "输油",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "gas",
              label: "燃气",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "electricity",
              label: "电力",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "communication",
              label: "通信",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "waterProject",
              label: "水利",
              children: [
                {
                  value: "facility",
                  label: "受灾设施数",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
          ],
        },
        {
          value: "secondaryDisaster",
          label: "次生灾害",
          children: [
            {
              value: "crumble",
              label: "崩塌",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "landslip",
              label: "滑坡",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "debrisFlow",
              label: "泥石流",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "lava",
              label: "熔岩塌陷",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "fissure",
              label: "地裂缝",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "subsidence",
              label: "地面沉降",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
            {
              value: "others",
              label:
                "其他(沙土液化、火灾、毒气泄漏、爆炸、环境污染、瘟疫、海啸等)",
              children: [
                {
                  value: "loss",
                  label: "受灾损失",
                },
                {
                  value: "range",
                  label: "受灾范围",
                },
                {
                  value: "extent",
                  label: "受灾程度",
                },
              ],
            },
          ],
        },
      ],
    };
  },

  methods: {
    handleChange(value) {
      console.log(value);
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
};
</script>

<style>
</style>