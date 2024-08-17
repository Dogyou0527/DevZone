---
title: ROS

---

# 學習ROS
[別人的共筆](https://hackmd.io/@nthu-ditrobotics/Hyem5Kj6o)
ros運行於linux需要虛擬機，我用virtualbox
## 安裝

- [安裝步驟](https://github.com/sutd-robotics/virtualbox-ubuntu-ros?tab=readme-ov-file#1-Installing-Virtualbox)
- 直接安裝付ubuntu的virtualbox [連結](https://www.osboxes.org/ubuntu/#ubuntu-20-04-4-vbox)
    - 使用vid檔當作vm的硬碟，就直接是ubuntu了
    - 可以在創建機器時選擇版本![螢幕擷取畫面 2024-08-05 225947](https://hackmd.io/_uploads/HyvVFwAYA.png)
    - 使用檢視中的縮放模式比較好用，但要記得 right control + home 可以叫出菜單

- 

### 問題
* amd cpu 需要在bios打開svm的設定，否則虛擬機開不起來

- 全螢幕只有1/4內容
    - 使用視窗化模式
- 沒有複製貼上
    - 在一般設定中的剪貼簿打開雙向的選項
- 在ubuntu24.04中安裝不起來
    - 安裝推薦的20.04
- 使用不了硬碟檔
    - 要先加入新的，否則他有一個預設的
        - 使用者名稱： osboxes
        - 密碼： osboxes.org
![螢幕擷取畫面 2024-08-05 230729](https://hackmd.io/_uploads/HJikjvAY0.png)

## 基本設置
### 照gpt說的做
安裝ROS之後，你可以進行一系列配置和基本操作，以便開始使用和開發ROS應用程序。以下是安裝ROS之後的基本步驟和推薦操作：

### 1. 設置環境變數

每次打開一個新的終端窗口時，你需要重新設置ROS的環境變數。為了簡化這個過程，可以將設置環境變數的命令添加到你的`.bashrc`文件中。

1. **打開終端並編輯 `.bashrc` 文件**：
   ```bash
   gedit ~/.bashrc
   ```

2. **在文件末尾添加以下行**：
   ```bash
   source /opt/ros/<distro>/setup.bash
   ```
   將 `<distro>` 替換為你安裝的ROS版本，如`noetic`或`humble`。

3. **保存並關閉 `.bashrc` 文件**，然後重新加載該文件：
   ```bash
   source ~/.bashrc
   ```

### 2. 初始化 `rosdep`

`rosdep` 是一個ROS工具，用於安裝系統依賴項。初次使用時需要初始化它。

1. **初始化 `rosdep`**：
   ```bash
   sudo rosdep init
   rosdep update
   ```

### 3. 設置工作空間

ROS開發通常需要一個工作空間來存放源代碼和編譯文件。典型的工作空間叫做`catkin_ws`。

1. **創建工作空間目錄**：
   ```bash
   mkdir -p ~/catkin_ws/src
   ```

2. **導航到工作空間並初始化**：
   ```bash
   cd ~/catkin_ws/
   catkin_make
   ```

3. **設置工作空間的環境變數**：
   - 編輯`.bashrc`文件，再次添加以下行：
     ```bash
     source ~/catkin_ws/devel/setup.bash
     ```
   - 保存並執行以下命令以加載環境變數：
     ```bash
     source ~/.bashrc
     ```

### 4. 測試安裝

1. **啟動ROS核心**：
   - ROS核心是一個必要的背景進程，用於處理通信。運行以下命令來啟動它：
     ```bash
     roscore
     ```

2. **運行範例節點**：
   - 在一個新的終端中，運行以下命令來啟動範例的`talker`和`listener`節點：
     ```bash
     rosrun rospy_tutorials talker
     ```
   - 在另一個終端中：
     ```bash
     rosrun rospy_tutorials listener
     ```

3. **檢查話題和節點**：
   - 使用`rostopic list`來查看當前活躍的話題：
     ```bash
     rostopic list
     ```
   - 使用`rosnode list`來查看運行中的節點：
     ```bash
     rosnode list
     ```

### 5. 使用ROS工具

1. **`rviz`**：這是一個3D可視化工具，用於查看機器人的傳感器數據和狀態。
   - 啟動`rviz`：
     ```bash
     rosrun rviz rviz
     ```

2. **`rqt`**：這是一個圖形化工具，可以顯示和控制ROS節點、話題、服務和參數。
   - 啟動`rqt`：
     ```bash
     rosrun rqt_gui rqt_gui
     ```

### 6. 開始開發

1. **編寫ROS節點**：
   - 開始學習如何使用Python（`rospy`）或C++（`roscpp`）編寫ROS節點。你可以參考官方的[Python教程](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29)或[C++教程](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c++%29)。

2. **創建和構建自己的包**：
   - 在你的工作空間中創建一個新的ROS包：
     ```bash
     cd ~/catkin_ws/src
     catkin_create_pkg my_package std_msgs rospy roscpp
     ```
   - 編譯工作空間：
     ```bash
     cd ~/catkin_ws
     catkin_make
     ```

3. **學習使用模擬器**：
   - 安裝和使用Gazebo等模擬器來測試你的機器人應用程序。

### 7. 繼續學習和探索

- **學習進階主題**：探索導航、SLAM、機器人視覺等高級主題。
- **參與社區**：加入ROS社區，參與討論，解決問題，並與他人合作。
- **參加課程和工作坊**：尋找相關的線上或線下培訓課程以加速學習。

通過這些步驟，你可以熟悉ROS的基本使用並逐步深入到更複雜的機器人開發中。保持實踐和學習是掌握ROS的關鍵。

## 基本概念

### GPT
了解ROS的基本概念是開始使用和開發機器人應用的關鍵。以下是ROS中的一些核心概念：

### 1. **節點（Nodes）**

- **定義**：節點是ROS中執行計算的進程。每個節點通常負責一個特定的功能或任務，如控制電機、處理傳感器數據等。
- **特點**：節點之間可以通過主題、服務或行動來通信。這種設計使得系統更加模塊化和靈活。
- **示例**：一個節點可以是相機數據的發布者，另一個節點可以是數據處理器。

### 2. **主題（Topics）**

- **定義**：主題是節點之間傳輸數據的通道。它們是一種發布-訂閱通信模型，允許一個或多個發布者（publishers）將數據發送到一個或多個訂閱者（subscribers）。
- **特點**：主題無需發布者和訂閱者之間的直接連接，這使得系統更具擴展性和靈活性。
- **示例**：`/camera/image` 主題可以用於傳輸相機圖像數據，`/cmd_vel` 主題可以用於傳輸機器人的速度命令。

### 3. **消息（Messages）**

- **定義**：消息是主題中傳遞的數據結構。每個消息都是由特定類型定義的數據結構，可以包括多種基本數據類型（如整數、浮點數）以及其他消息類型。
- **特點**：ROS提供了多種標準消息類型（如`std_msgs`、`sensor_msgs`），也支持自定義消息類型。
- **示例**：`std_msgs/String` 是一個簡單的字符串消息類型，`sensor_msgs/Image` 用於傳輸圖像數據。

### 4. **服務（Services）**

- **定義**：服務是一種請求-響應通信模型，允許一個節點向另一個節點發送請求並接收回應。這與主題的發布-訂閱模式不同，因為它是同步的。
- **特點**：服務由兩部分組成：服務服務器（提供者）和服務客戶端（請求者）。服務的定義包括請求和響應的消息結構。
- **示例**：一個服務可以用來查詢機器人的狀態，請求可能是 `GetStatus`，響應是當前狀態的描述。

### 5. **行動（Actions）**

- **定義**：行動是一種可以跟蹤長時間運行任務進度的通信方式。它允許客戶端發送目標，並接收目標達成的狀態更新。
- **特點**：行動由目標（goal）、反饋（feedback）和結果（result）三部分組成。它適合用於需要長時間執行的任務，如導航。
- **示例**：機器人導航到某一位置的任務可以通過行動來實現，期間可以持續更新導航的進展。

### 6. **參數伺服器（Parameter Server）**

- **定義**：參數伺服器是ROS核心的一部分，用於存儲和檢索參數。參數可以是全局的，並且可供多個節點使用。
- **特點**：參數伺服器支持節點動態設置和獲取參數，這對於配置和調試系統非常有用。
- **示例**：機器人的最大速度、傳感器的校準數據等可以存儲在參數伺服器上。

### 7. **ROS Master**

- **定義**：ROS Master是ROS系統中的中央協調組件，負責管理節點的註冊、主題和服務的名稱空間。
- **特點**：每個ROS系統必須有一個Master，通常由`roscore`命令啟動。
- **功能**：Master幫助節點發現彼此，並建立彼此之間的通信。

### 8. **包（Packages）**

- **定義**：包是ROS軟件的基本單位，它們包含節點、消息、服務和其他文件。包用於組織代碼、數據和資源。
- **特點**：每個包都有一個唯一的名稱和相關的包描述文件（`package.xml`）和構建文件（如`CMakeLists.txt`）。
- **示例**：常見的ROS包包括`geometry_msgs`、`nav_msgs`等，它們提供了基本的消息類型和工具。

### 9. **工作空間（Workspaces）**

- **定義**：工作空間是一個目錄結構，用於組織和管理ROS包。它允許開發者進行開發、構建和安裝包。
- **特點**：工作空間通常包含 `src` 目錄（存放源代碼）、`build` 目錄（編譯生成的中間文件）、`devel` 目錄（開發時使用的生成文件）和 `install` 目錄（安裝的文件）。
- **示例**：`catkin_ws` 是一個常用的工作空間名稱。

了解並熟悉這些基本概念後，你就能夠更好地理解和使用ROS系統，開發各種機器人應用。這些概念的具體實現和使用方法可以通過官方教程和文檔進一步學習。

### 疑問
- 主題(topics)和服務(services)的差別
    - 節點發消息到主題時，不用等訂閱者回復，可以直接繼續下一行，而且可以多對多；而服務則相反，會阻塞、要確認、一對一。
- Message 是幹嘛的
    - 主題（Topics）和服務（Services）在ROS中都依賴於消息（Messages）來進行數據傳遞

## 範例
當然！下面是一個簡單的ROS示例，包括創建一個發布者節點和一個訂閱者節點。這些節點將在一個主題上進行通信，發布者節點將在主題上發送消息，而訂閱者節點將接收這些消息並打印出來。

### 1. **設置工作空間**

首先，確保你有一個ROS工作空間。你可以創建一個新的工作空間並構建它：

```bash
# 創建工作空間
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/

# 構建工作空間
catkin_make
```

### 2. **創建ROS包**

在工作空間的 `src` 目錄下創建一個新的ROS包，並指定依賴的ROS包（例如 `rospy` 和 `std_msgs`）：

```bash
cd ~/catkin_ws/src
catkin_create_pkg my_package std_msgs rospy
```

這將創建一個名為 `my_package` 的包。

### 3. **編寫發布者節點**

在 `my_package` 目錄下創建 `scripts` 目錄並編寫一個名為 `talker.py` 的發布者節點：

```bash
cd ~/catkin_ws/src/my_package
mkdir scripts
touch scripts/talker.py
chmod +x scripts/talker.py
```

編輯 `talker.py` 文件：

```python
#!/usr/bin/env python

import rospy
from std_msgs.msg import String

def talker():
    pub = rospy.Publisher('chatter', String, queue_size=10)
    rospy.init_node('talker', anonymous=True)
    rate = rospy.Rate(1) # 1 Hz
    while not rospy.is_shutdown():
        hello_str = "hello world %s" % rospy.get_time()
        rospy.loginfo(hello_str)
        pub.publish(hello_str)
        rate.sleep()

if __name__ == '__main__':
    try:
        talker()
    except rospy.ROSInterruptException:
        pass
```

這個節點每秒（1 Hz）向名為 `chatter` 的主題發布一個字符串消息。

### 4. **編寫訂閱者節點**

同樣，在 `scripts` 目錄下創建一個名為 `listener.py` 的訂閱者節點：

```bash
touch scripts/listener.py
chmod +x scripts/listener.py
```

編輯 `listener.py` 文件：

```python
#!/usr/bin/env python

import rospy
from std_msgs.msg import String

def callback(data):
    rospy.loginfo(rospy.get_caller_id() + " I heard %s", data.data)

def listener():
    rospy.init_node('listener', anonymous=True)
    rospy.Subscriber('chatter', String, callback)
    rospy.spin()

if __name__ == '__main__':
    listener()
```

這個節點訂閱 `chatter` 主題並在接收到消息時打印它。

### 5. **編譯包**

回到工作空間的根目錄並編譯包：

```bash
cd ~/catkin_ws
catkin_make
```

### 6. **運行節點**

首先啟動 `roscore`：

```bash
roscore
```

然後在另一個終端中運行發布者和訂閱者節點：

```bash
# 運行發布者節點
source devel/setup.bash
rosrun my_package talker.py
```

```bash
# 運行訂閱者節點
source devel/setup.bash
rosrun my_package listener.py
```

你應該會在`talker.py`的終端中看到發佈的消息，以及在`listener.py`的終端中看到接收到的消息。

這個簡單的示例展示了如何使用ROS的發布-訂閱模型來進行節點間通信。你可以基於這個基礎進行更複雜的開發，並探索更多的ROS功能和工具。
 
 ### 結果
 成功發出和接收，中間遇到
 /usr/bin/env: ‘python’: No such file or directory
 的問題，好像是遇到ros喜歡python 2 但我只有3 的問題，最後是用
 sudo ln -s /usr/bin/python3 /usr/bin/python
 將python 連結到python3 來解決，之後遇到問題再說
 
 
## URDF

>  ### GPT
> 創建一個簡單的機器人模型（例如一個兩輪車）並在 `rviz` 中進行可視化是學習 ROS 中 Unified Robot Description Format (URDF) 的理想起點。以下是詳細步驟和說明，幫助你完成這個專案。
> 
> ### 專案目標
> 
> - **學習 URDF 的基本語法和結構**：理解如何使用 URDF 文件來描述機器人的連接、關節和外觀。
> - **在 `rviz` 中可視化機器人模型**：學習如何使用 `rviz` 來查看和檢查機器人的模型和運動。
> 
> ### 前置需求
> 
> - 基本的 ROS 和 Linux 命令操作知識。
> - 已經安裝並配置好 ROS 環境。
> - 已經安裝 `rviz`（如果還沒有，請使用 `sudo apt-get install ros-<distro>-rviz` 安裝，將 `<distro>` 替換為你的 ROS 發行版）。
> 
> ### 步驟 1：設置工作空間
> 
> 1. **創建一個新的 ROS 工作空間（如果你還沒有）**：
> 
>    ```bash
>    mkdir -p ~/catkin_ws/src
>    cd ~/catkin_ws/
>    catkin_make
>    source devel/setup.bash
>    ```
> 
> 2. **創建一個新的 ROS 包**：
> 
>    ```bash
>    cd ~/catkin_ws/src
>    catkin_create_pkg my_robot_description urdf rviz
>    ```
> 
>    這個包名為 `my_robot_description`，並且依賴於 `urdf` 和 `rviz`。
> 
> ### 步驟 2：編寫 URDF 文件
> 
> 1. **在包中創建一個 `urdf` 目錄來存放機器人描述文件**：
> 
>    ```bash
>    mkdir -p ~/catkin_ws/src/my_robot_description/urdf
>    ```
> 
> 2. **編寫 URDF 文件**：
> 
>    使用你喜歡的編輯器創建並編輯 `my_robot.urdf` 文件：
> 
>    ```bash
>    gedit ~/catkin_ws/src/my_robot_description/urdf/my_robot.urdf
>    ```
> 
>    在這個文件中，描述一個簡單的兩輪機器人模型：
> 
>    ```xml
>    <robot name="my_robot">
>      <link name="base_link">
>        <visual>
>          <geometry>
>            <box size="0.5 0.5 0.1" />
>          </geometry>
>          <material name="blue">
>            <color rgba="0 0 1 1" />
>          </material>
>        </visual>
>      </link>
> 
>      <link name="wheel_left">
>        <visual>
>          <geometry>
>            <cylinder length="0.1" radius="0.1" />
>          </geometry>
>          <origin xyz="-0.2 0.3 0" rpy="0 1.5708 0" />
>          <material name="black">
>            <color rgba="0 0 0 1" />
>          </material>
>        </visual>
>      </link>
> 
>      <link name="wheel_right">
>        <visual>
>          <geometry>
>            <cylinder length="0.1" radius="0.1" />
>          </geometry>
>          <origin xyz="-0.2 -0.3 0" rpy="0 1.5708 0" />
>          <material name="black">
>            <color rgba="0 0 0 1" />
>          </material>
>        </visual>
>      </link>
> 
>      <joint name="left_wheel_joint" type="continuous">
>        <parent link="base_link" />
>        <child link="wheel_left" />
>        <origin xyz="0 0.3 0" />
>        <axis xyz="0 1 0" />
>      </joint>
> 
>      <joint name="right_wheel_joint" type="continuous">
>        <parent link="base_link" />
>        <child link="wheel_right" />
>        <origin xyz="0 -0.3 0" />
>        <axis xyz="0 1 0" />
>      </joint>
>    </robot>
>    ```
> 
>    - **`<link>`**：定義機器人的部件。在這裡，我們定義了 `base_link` 作為機器人的底座，以及兩個輪子 `wheel_left` 和 `wheel_right`。
>    - **`<visual>`**：定義機器人部件的外觀，包含形狀和顏色。
>    - **`<joint>`**：定義機器人部件之間的連接方式。在這裡，我們使用連續的關節來描述輪子的自由旋轉。
> 
> ### 步驟 3：在 `rviz` 中可視化
> 
> 1. **啟動 `rviz`**：
> 
>    ```bash
>    rosrun rviz rviz
>    ```
> 
> 2. **加載 URDF 文件**：
> 
>    - 在 `rviz` 的左側面板中，點擊 `Add` 按鈕。
>    - 在彈出的窗口中選擇 `RobotModel`，然後點擊 `OK`。
>    - 在左側的 `Displays` 面板中，找到 `RobotModel`，在 `Description` 欄位中輸入 URDF 文件的路徑，如下：
> 
>      ```bash
>      $(find my_robot_description)/urdf/my_robot.urdf
>      ```
> 
> 3. **設定固定框架**：
> 
>    確保 `Fixed Frame` 設置為 `base_link` 或你在 URDF 中定義的主框架（例如 `map` 或 `odom`，根據需要調整）。
> 
> 4. **檢查模型**：
> 
>    如果一切正確，你應該能夠在 `rviz` 的視圖窗口中看到你創建的兩輪機器人模型。你可以旋轉視圖、放大縮小來檢查模型的各個部分。
> 
> ### 步驟 4：擴展專案
> 
> 1. **添加更多的部件**：
>    - 例如，你可以為機器人添加一個相機、雷達或其他感測器。
> 
> 2. **模擬運動**：
>    - 嘗試使用 `joint_state_publisher` 和 `robot_state_publisher` 來模擬機器人關節的運動。
> 
> 3. **導入 Mesh 文件**：
>    - 將自定義的 3D 模型（如 `.dae` 或 `.stl` 文件）導入 URDF，以替代基本的幾何形狀。
> 
> 4. **添加碰撞和慣性**：
>    - 在 URDF 中定義機器人的碰撞屬性和慣性矩，以便在物理模擬中使用。
> 
> ### 結語
> 
> 這個專案為你提供了學習 ROS 中 URDF 的基礎知識和技能，並且為進一步的機器人建模和仿真奠定了基礎。通過擴展這個專案，你可以逐步建立更為複雜和真實的機器人模型。
>  

![螢幕擷取畫面 2024-08-11 080658](https://hackmd.io/_uploads/SyaTeFBcA.png)
## bug
無法用gpt的方法打開，需要使用launch打開
### gpt
> 創建一個啟動文件，將 URDF 文件的內容設置為 ROS 參數 robot_description，並啟動 RViz 來加載這個機器人模型。
> 
> bash
> 
> mkdir -p ~/catkin_ws/src/my_robot_description/launch
> gedit ~/catkin_ws/src/my_robot_description/launch/display.launch
> 在這個啟動文件中添加以下內容：
> 
> xml
> <launch>
>   <!-- 加載並設置 URDF 文件為 robot_description 參數 -->
>   <param name="robot_description" command="$(find xacro)/xacro '$(find my_robot_description)/urdf/my_robot.urdf'" />
> 
>   <!-- 啟動 RViz 並加載自定義的 RViz 設定檔 -->
>   <node name="rviz" pkg="rviz" type="rviz" args="-d $(find my_robot_description)/rviz/my_robot.rviz" />
> </launch>
> 步驟 3：創建 RViz 設定檔
> 確保有一個 RViz 設定檔，用於定義 RViz 的顯示項。你可以參考之前提供的範例創建一個 my_robot.rviz 文件。
> 
> 步驟 4：啟動 Launch 文件
> 在終端中運行以下命令來啟動該文件：
> 
> bash
> 
> roslaunch my_robot_description display.launch

### 實作
在這之中，my_robot_description 是package需要符合package的架構(描述文件（package.xml）和構建文件（如CMakeLists.txt）)
使用
```
rospack list | grep my_robot_description
```
發現沒有my_robot這個包
此外還需要有rviz的config檔
原本不存在，可以用新的rviz將config存出來

## 動起來
嘗試讓urdf能動
### 經歷
rviz收不到topic的訊息
- 產生一個包做控制節點

tree
```
CMakeLists.txt -> /opt/ros/noetic/share/catkin/cmake/toplevel.cmake
├── frames.gv
├── my_package
│   ├── CMakeLists.txt
│   ├── package.xml
│   ├── scripts
│   │   ├── listener.py
│   │   └── talker.py
│   └── src
├── my_robot_control
│   ├── CMakeLists.txt
│   ├── config
│   │   └── controller.yaml
│   ├── launch
│   │   └── controller.launch
│   ├── package.xml
│   ├── scripts
│   │   └── control_node.py
│   └── src
└── my_robot_description
    ├── CMakeLists.txt
    ├── launch
    │   └── display.launch
    ├── package.xml
    ├── rviz
    │   ├── my_robot1.rviz
    │   └── my_robot.rviz
    └── urdf
        └── my_robot.urdf
```

```
$ cat config/controller.yaml 

left_wheel_controller:
  type: effort_controllers/JointPositionController
  joint: left_wheel_joint
  pid: {p: 100.0, i: 0.1, d: 0.0, i_clamp: 1.0}

right_wheel_controller:
  type: effort_controllers/JointPositionController
  joint: right_wheel_joint
  pid: {p: 100.0, i: 0.1, d: 0.0, i_clamp: 1.0}
```
urdf
```
$ cat my_robot_description/urdf/my_robot.urdf 
<robot name="my_robot">
  <link name="base_link">
    <visual>
      <geometry>
        <box size="0.5 0.5 0.1" />
      </geometry>
      <material name="blue">
        <color rgba="0 0 1 1" />
      </material>
    </visual>
  </link>

  <link name="wheel_left">
    <visual>
      <geometry>
        <cylinder length="0.1" radius="0.1" />
      </geometry>
      <origin xyz="-0.2 0.3 0" rpy="0 1.5708 0" />
      <material name="black">
        <color rgba="0 0 0 1" />
      </material>
    </visual>
  </link>

  <link name="wheel_right">
    <visual>
      <geometry>
        <cylinder length="0.1" radius="0.1" />
      </geometry>
      <origin xyz="-0.2 -0.3 0" rpy="0 1.5708 0" />
      <material name="black">
        <color rgba="0 0 0 1" />
      </material>
    </visual>
  </link>

  <joint name="left_wheel_joint" type="continuous">
    <parent link="base_link" />
    <child link="wheel_left" />
    <origin xyz="0 0.3 0" />
    <axis xyz="0 1 0" />
  </joint>

  <joint name="right_wheel_joint" type="continuous">
    <parent link="base_link" />
    <child link="wheel_right" />
    <origin xyz="0 -0.3 0" />
    <axis xyz="0 1 0" />
  </joint>

  <!-- Add transmissions for each joint -->
  <transmission name="left_wheel_transmission">
    <type>transmission_interface/SimpleTransmission</type>
    <joint name="left_wheel_joint">
      <hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
    </joint>
    <actuator name="left_wheel_actuator">
      <hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
    </actuator>
  </transmission>

  <transmission name="right_wheel_transmission">
    <type>transmission_interface/SimpleTransmission</type>
    <joint name="right_wheel_joint">
      <hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
    </joint>
    <actuator name="right_wheel_actuator">
      <hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
    </actuator>
  </transmission>
</robot>
```
controller.launch
```
$ cat launch/controller.launch 
<launch>
  <!-- Load the controllers -->
  <rosparam file="$(find my_robot_control)/config/controller.yaml" command="load" />

  <!-- Start the controllers -->
  <node name="controller_spawner" pkg="controller_manager" type="spawner" respawn="false" output="screen">
    <param name="controllers" type="yaml" value="$(find my_robot_control)/config/controller.yaml" />
  </node>
</launch>
```
rviz launch
```
 cat my_robot_description/launch/display.launch 
<launch>
    <!-- 加載 URDF 文件 -->
    <param name="robot_description" command="$(find xacro)/xacro $(find my_robot_description)/urdf/my_robot.urdf" />

    <!-- 啟動 robot_state_publisher 節點 -->
    <node name="robot_state_publisher" pkg="robot_state_publisher" type="robot_state_publisher" />

    <!-- 啟動 Rviz 以視覺化 URDF -->
    <node name="rviz" pkg="rviz" type="rviz" args="-d $(find my_robot_description)/config/my_robot.rviz" />
</launch>

```
![螢幕擷取畫面 2024-08-11 204033](https://hackmd.io/_uploads/BkpPbVIcR.png)

## gazebo
[安裝教學](https://gazebosim.org/docs/garden/install_ubuntu/)
啟動gazebo時打不開
```
gz sim shapes.sdf
```
問gpt報錯訊息後，打開vm的3d加速選項
[範例](https://github.com/gazebosim/gz-sim/tree/main)

ros 1 不支援gazebo garden
改用citadel 但會閃


# linux useful commands
顯示目錄樹
```
tree 
```
顯示目錄
```
ls
```
進入目錄
```
cd
cd ..
cd ../..
```
編輯器
```
gedit
```


