# 🏗️ 项目重构代码结构

## 📁 新的项目结构
```
src/
├── vision/                 # 替换原audio模块
│   ├── __init__.py
│   ├── camera_analyzer.py  # 摄像头分析器
│   ├── motion_detector.py  # 运动检测
│   ├── color_analyzer.py   # 颜色分析
│   └── object_detector.py  # 物体识别
├── ai/                     # 新增AI模块
│   ├── __init__.py
│   ├── text_processor.py   # 文字处理
│   ├── style_generator.py  # 风格生成器
│   └── prompt_parser.py    # 提示词解析
├── ui/
│   ├── creative_studio.py  # 重构：摄像头+AI工作室
│   ├── camera_gallery.py   # 重构：摄像头画廊
│   └── text_input.py       # 新增：文字输入界面
├── visualization/
│   ├── vision_engine.py    # 重构：基于视觉的渲染引擎
│   └── ai_effects.py       # 新增：AI驱动的视觉效果
└── storage/
    └── manager.py          # 保持：数据存储(保存视频+文字)
```

## 🔄 核心类设计

### 1. VisionAnalyzer (替换AudioAnalyzer)
```python
class VisionAnalyzer:
    def __init__(self, camera_id=0, resolution=(1280, 720)):
        self.cap = cv2.VideoCapture(camera_id)
        self.motion_detector = MotionDetector()
        self.color_analyzer = ColorAnalyzer()
        self.object_detector = ObjectDetector()
        
        # 分析数据
        self.motion_intensity = 0.0
        self.dominant_colors = []
        self.detected_objects = []
        self.visual_energy = 0.0
        
    def capture_frame(self):
        """捕捉摄像头帧"""
        
    def analyze_motion(self, frame):
        """分析运动强度和方向"""
        
    def analyze_colors(self, frame):
        """分析主要颜色和分布"""
        
    def detect_objects(self, frame):
        """检测和识别物体"""
        
    def get_visual_metrics(self):
        """获取视觉指标(类似audio metrics)"""
        return {
            'motion_intensity': self.motion_intensity,
            'dominant_colors': self.dominant_colors,
            'object_count': len(self.detected_objects),
            'visual_energy': self.visual_energy
        }
```

### 2. AITextProcessor (新增)
```python
class AITextProcessor:
    def __init__(self, use_local_model=True):
        self.style_library = self.load_style_presets()
        self.current_style = "default"
        
    def process_user_input(self, text_input):
        """处理用户文字输入"""
        
    def extract_style_keywords(self, text):
        """从文字中提取风格关键词"""
        
    def generate_visual_parameters(self, keywords):
        """将关键词转换为视觉参数"""
        
    def apply_realtime_style(self, visual_data, style_params):
        """实时应用风格到视觉数据"""
```

### 3. EnhancedParticleSystem (升级)
```python
class EnhancedParticleSystem:
    def __init__(self):
        self.vision_particles = []  # 基于视觉的粒子
        self.ai_particles = []      # AI生成的粒子
        
    def spawn_from_motion(self, motion_data):
        """根据运动数据生成粒子"""
        
    def spawn_from_colors(self, color_data):
        """根据颜色数据生成粒子"""
        
    def spawn_from_objects(self, object_data):
        """根据识别的物体生成粒子"""
        
    def apply_ai_style(self, style_params):
        """应用AI生成的风格"""
```

## 🎨 用户界面设计

### 主界面布局
```
┌─────────────────────────────────────────────┐
│ 🎥 Vision AI Creative Studio               │
├─────────────────────────────────────────────┤
│                                             │
│  ┌─────────────┐  ┌─────────────────────┐   │
│  │   Camera    │  │    Particle        │   │
│  │   Feed      │  │    Effects          │   │
│  │   (Live)    │  │    (AI Generated)   │   │
│  │             │  │                     │   │
│  └─────────────┘  └─────────────────────┘   │
│                                             │
│  ┌─────────────────────────────────────────┐ │
│  │ 💬 Text Input: "让粒子像火焰一样舞蹈"  │ │
│  └─────────────────────────────────────────┘ │
│                                             │
│  Style: [Fire] [Water] [Cyber] [Custom]    │
│  Motion: ████████░░ 80%                     │
│  Colors: 🔴🟡🟠 (detected)                  │
│  Objects: 👤 Person, ✋ Hand                │
└─────────────────────────────────────────────┘
```

## 🎯 实现策略

### Phase 1: 最小可行产品 (MVP)
**目标**: 基础摄像头 + 简单文字风格
```python
# 核心功能
1. 摄像头捕捉 ✓
2. 基础运动检测 ✓
3. 简单颜色分析 ✓
4. 文字输入界面 ✓
5. 预设风格应用 ✓

# 效果演示
"fire" → 红橙色粒子，向上运动
"water" → 蓝绿色粒子，流动效果
"space" → 深色背景，星星粒子
```

### Phase 2: AI增强
```python
# 高级功能
1. 物体识别 (YOLO)
2. 手势检测 (MediaPipe)
3. 自然语言处理
4. 动态风格生成
5. 实时风格转换
```

### Phase 3: 创意扩展
```python
# 艺术功能
1. 风格迁移网络
2. 3D粒子效果
3. 虚拟背景替换
4. 多摄像头支持
5. 云端AI集成
```

## ⚡ 技术细节

### 性能优化
- 多线程处理：摄像头捕捉 + 图像分析 + 渲染分离
- 帧率控制：30 FPS捕捉，60 FPS渲染
- 内存管理：循环缓冲区，及时释放图像数据
- GPU加速：OpenCV CUDA，可选PyTorch GPU推理

### 用户体验
- 实时反馈：<100ms延迟
- 平滑过渡：风格切换动画
- 智能提示：文字输入自动补全
- 错误恢复：摄像头断开自动重连

## 🎪 创意使用案例

1. **"让粒子跟随我的手"**
   - 手势检测 → 粒子跟随手部轨迹
   
2. **"变成梵高的星空"**
   - 风格转换 → 螺旋式粒子运动
   
3. **"我笑的时候变成彩虹"**
   - 表情识别 → 颜色渐变效果
   
4. **"水中的鱼"**
   - 物体检测 → 流体动画效果

你觉得这个设计如何？我们从哪个Phase开始实现比较好？