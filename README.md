# ROS2 Project

Bu proje, ROS2 kullanılarak geliştirilmiş bir robotik yazılım uygulamasıdır. Proje, düğümler (nodes), servisler (services), konular (topics) ve aksiyonlar (actions) üzerinden haberleşen modüler bir mimari sunar.

---

## Özellikler

- ROS2 tabanlı modüler mimari
- Publisher / Subscriber iletişimi
- Service ve Action kullanımı
- Parametre yönetimi
- Paketler arası bağımlılık yapısı
- Docker desteği ile kolay dağıtım
- Kolay genişletilebilir yapı

---

## Proje Yapısı

```
├── Dockerfile
├── docker-compose.yml
├── entrypoint.sh
├── launch
│   └── my_project.launch.py
└── src
    ├── command_server_pkg
    │   ├── CMakeLists.txt
    │   ├── command_server_pkg
    │   │   ├── __init__.py
    │   │   └── command_server.py
    │   ├── package.xml
    │   ├── setup.cfg
    │   └── srv
    │       └── ComputeCommand.srv
    ├── data_processor_pkg
    │   ├── data_processor_pkg
    │   │   ├── __init__.py
    │   │   └── data_processor.py
    │   ├── package.xml
    │   ├── resource
    │   │   └── data_processor_pkg
    │   ├── setup.cfg
    │   └── setup.py
    └── sensor_publisher_pkg
        ├── package.xml
        ├── resource
        │   └── sensor_publisher_pkg
        ├── sensor_publisher_pkg
        │   ├── __init__.py
        │   └── sensor_publisher.py
        ├── setup.cfg
        └── setup.py
```

---

## Kurulum

### Yerel Kurulum (Native)

#### 1. ROS2'yi Kurun

```bash
sudo apt update
sudo apt install ros-humble-desktop
```

#### 2. Workspace Oluşturun

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
```

#### 3. Projeyi Klonlayın

```bash
cd ~/ros2_ws/src
git clone https://github.com/devemresr/ros2_homework
```

#### 4. Derleyin

```bash
cd ~/ros2_ws
colcon build
source install/setup.bash
```

### Docker ile Kurulum

#### 1. Docker İmajını Oluşturun

```bash
docker build -t ros2_project .
```

#### 2. Container'ı Çalıştırın

```bash
docker run -it --rm ros2_project
```

#### 3. Docker Compose ile Çalıştırın (Önerilir)

```bash
docker-compose up
```

---

## Çalıştırma

### Paket Çalıştırma

```bash
ros2 run your_package your_node
```

#### Örnek:

```bash
ros2 run sensor_publisher_pkg sensor_publisher
ros2 run data_processor_pkg data_processor
ros2 run command_server_pkg command_server
```

### Launch Dosyası Çalıştırma

```bash
ros2 launch your_package your_launch_file.launch.py
```

#### Tüm Sistemi Çalıştırma:

```bash
ros2 launch launch/my_project.launch.py
```

---

## Test

### Tüm Testleri Çalıştırma

```bash
colcon test
colcon test-result --verbose
```

### Belirli Bir Paketi Test Etme

```bash
colcon test --packages-select your_package
```

---

## ROS2 Komutları

### Topics Kontrolü

```bash
# Tüm topic'leri listele
ros2 topic list

# Topic'ten gelen verileri görüntüle
ros2 topic echo /your_topic

# Topic hakkında bilgi al
ros2 topic info /your_topic

# Topic'e veri yayınla
ros2 topic pub /your_topic std_msgs/msg/String "data: 'test'"
```

### Node Kontrolü

```bash
# Çalışan node'ları listele
ros2 node list

# Node hakkında bilgi al
ros2 node info /your_node
```

### Service Kontrolü

```bash
# Servisleri listele
ros2 service list

# Servis çağır
ros2 service call /your_service your_package/srv/YourService "{field: value}"
```

### Parametreler

```bash
# Tüm parametreleri listele
ros2 param list

# Parametre değerini görüntüle
ros2 param get /your_node param_name

# Parametre değerini değiştir
ros2 param set /your_node param_name value

# Parametreleri dosyaya kaydet
ros2 param dump /your_node
```

---

## Paket Açıklamaları

### sensor_publisher_pkg

Sensör verilerini yayınlayan düğüm. Belirli aralıklarla veri üretir ve topic üzerinden yayınlar.

### data_processor_pkg

Sensör verilerini işleyen düğüm. Subscribe olduğu topic'ten veri alır, işler ve sonuçları yayınlar.

### command_server_pkg

Komut işleme servisi. Gelen servisleri işler ve hesaplama yapar.

---

## Geliştirme

### Yeni Paket Oluşturma

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python your_new_package
```

### Değişiklikleri Derleme

```bash
cd ~/ros2_ws
colcon build --packages-select your_package
source install/setup.bash
```

---

## Sorun Giderme

### Kaynak Dosyalarını Yükleme Sorunu

```bash
source /opt/ros/humble/setup.bash
source ~/ros2_ws/install/setup.bash
```

### Bağımlılık Sorunları

```bash
cd ~/ros2_ws
rosdep install --from-paths src --ignore-src -r -y
```

### Build Sorunları

```bash
# Workspace'i temizle ve tekrar derle
cd ~/ros2_ws
rm -rf build install log
colcon build
```

---
