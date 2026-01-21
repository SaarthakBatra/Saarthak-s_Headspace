# Raspberry Pi 4 BAM System – Complete Setup Guide
**Phase 1: Hardware Configuration & Initial Picamera2 Setup**

**For:** Raspberry Pi 4 Model B 4GB | HQ Camera | 32GB microSD | Fedora KDE Plasma Development System  
**Target:** 5-10 minute BAM capture sessions, Phase 1 baseline, Option A (microSD-only initial)  
**Date:** January 21, 2026

---

## PART 1: MICROSD CARD SELECTION & PREPARATION

### 1.1 Recommended MicroSD Card
Your current 32GB UHS-I card (120MB/s) is **suitable for initial debugging**, but for permanent use, upgrade to:

| Metric | Recommended Card | Your Current Card | Status |
|--------|------------------|-------------------|--------|
| **Capacity** | 64GB (future-proof OS room) | 32GB | Acceptable for Phase 1 |
| **Interface** | UHS-I (Pi4 max) | UHS-I | ✓ Correct |
| **Speed Grade** | V30 minimum (30 MB/s sustained) | Up to 120MB/s | ✓ Sufficient |
| **Brand** | Kingston Canvas React or Samsung Evo Plus | Generic/Unknown | Upgrade for production |
| **Price (India)** | ₹400-600 (~$5-7) | — | Budget-friendly |

**Why UHS-II won't help:** Raspberry Pi 4 **only supports UHS-I** via its microSD slot. UHS-II drives work but at UHS-I speeds (104 MB/s max), providing no benefit. Save your money.

**Order from:** Amazon India, Flipkart, or authorized retailers. Delivery typically 2-3 days.

### 1.2 Flashing Raspberry Pi OS Bookworm 64-bit

**Why Bookworm?** Latest libcamera stack, best Picamera2 support, 64-bit performance for future phases.

#### Step 1: Download and Flash
1. Download **Raspberry Pi Imager** from https://www.raspberrypi.com/software/
2. Insert microSD into your Fedora laptop via USB adapter
3. Launch **Raspberry Pi Imager**
4. Select:
   - **Device:** Raspberry Pi 4
   - **OS:** Raspberry Pi OS (Other) → Raspberry Pi OS (64-bit) Bookworm
   - **Storage:** Your microSD card
5. Click **Next**, accept defaults, click **Write**
6. Wait 5-10 minutes for completion

#### Step 2: First Boot Configuration
1. **Power off Pi**, insert flashed microSD, plug in HDMI monitor + USB keyboard/mouse + power
2. **Wait 60 seconds** for first boot (Raspberry Pi logo appears)
3. **Initial setup wizard** appears:
   - Language: English (or your preference)
   - WiFi: Select your lab network, enter password
   - Username/Password: `pi` / (set a strong password)
   - Set timezone: Asia/Kolkata
   - System update: Let it run (~5-10 minutes)
4. **Reboot** when prompted

---

## PART 2: RASPBERRY PI HARDWARE CONFIGURATION

### 2.1 Enable CSI Camera Port
After reboot:
```bash
sudo raspi-config
```

Navigate:
- **Interface Options** → **Legacy Camera** → Enable (if prompts)
- **Interface Options** → **Camera** → Enable
- **GPU Memory** → Set to **256MB** (for HQ camera processing)

Exit and **Reboot**.

### 2.2 Physically Connect HQ Camera

**⚠️ CRITICAL: Power off Pi completely before proceeding**

#### Ribbon Cable Orientation (Most Common Error!)

1. **Locate CSI port:** Between Ethernet (left) and HDMI (right) ports. **NOT** the DISPLAY port.
2. **Open CSI connector:** Gently pull **plastic tabs upwards, then towards Ethernet port**
3. **Prepare ribbon:**
   - Hold HQ camera ribbon cable
   - Identify shiny/copper side (contacts)
4. **Insert cable:**
   - **Contacts face TOWARDS HDMI port** (this is critical)
   - Push firmly until it seats at the bottom
   - You'll hear/feel a subtle click
5. **Close connector:** Push plastic tabs down and away from Ethernet
6. **Verify:** Ribbon is straight, horizontal, fully seated

**Visual check:**
- ✓ Ribbon appears level and symmetric in connector
- ✓ No visible gaps between ribbon and connector edges
- ✓ Plastic clip is fully closed
- ✗ If tilted or loose → re-seat it

#### Connect C-Mount Lens
1. Unscrew HQ camera lens mount (if standard lens attached)
2. Attach your C-mount lens (align red dots on lens and camera body)
3. Tighten gently (¼ turn past hand-tight)
4. **Do NOT force** — C-mount is delicate

#### Optional: Thermal Management
For sustained capture (Phase 1 testing):
- Attach official aluminum heatsink to Pi CPU (~$3, improves thermal performance)
- Do NOT add fan yet (noise/vibration concerns for BAM)

### 2.3 Boot and Verify Camera

1. **Power on Pi**, wait for desktop
2. Open **Terminal** and run:
```bash
libcamera-hello --timeout 3
```

**Expected output:**
- Camera preview window appears for 3 seconds
- Shows live image from your setup
- Terminal shows: `[timestamp] Camera 'imx477' started`

**If preview doesn't appear:**
- Check CSI ribbon seating (most common issue)
- Verify camera is enabled in raspi-config
- Reboot Pi
- Try again

---

## PART 3: PICAMERA2 INSTALLATION & RAW CAPTURE

### 3.1 Install Picamera2 Library

SSH into Pi from Fedora terminal, or use Pi terminal directly:

```bash
sudo apt install -y python3-picamera2
```

Verify installation:
```bash
python3 -c "from picamera2 import Picamera2; print('✓ Picamera2 ready')"
```

### 3.2 Test Raw Capture (Single Image)

Create file `capture_raw_test.py`:

```python
#!/usr/bin/env python3
from picamera2 import Picamera2
import time

print("[1] Initializing Picamera2...")
picam2 = Picamera2()

print("[2] Creating raw capture configuration...")
config = picam2.create_still_configuration(raw={})
picam2.configure(config)

print("[3] Starting camera, waiting 2 seconds for autofocus...")
picam2.start()
time.sleep(2)

print("[4] Capturing DNG raw image...")
request = picam2.capture_request()

# Save both JPEG and DNG for comparison
request.save("test_image.jpg")       # JPEG for quick preview
request.save_dng("test_image.dng")   # Raw 10-bit SGBRG for analysis

print("[5] Stopping camera...")
request.release()
picam2.stop()

# Check file sizes
import os
jpg_size = os.path.getsize("test_image.jpg") / 1024 / 1024
dng_size = os.path.getsize("test_image.dng") / 1024 / 1024
print(f"\n✓ Capture complete!")
print(f"   JPEG: {jpg_size:.2f} MB (compressed)")
print(f"   DNG:  {dng_size:.2f} MB (raw 10-bit SGBRG)")
```

Run it:
```bash
python3 capture_raw_test.py
```

**Expected output:**
- Files `test_image.jpg` and `test_image.dng` created in same directory
- DNG file ~18-19 MB (full 4056×3040 resolution)
- JPEG file ~2-4 MB

### 3.3 Test Raw Video Capture (5 seconds, Low Frame Rate)

Create file `capture_raw_video.py`:

```python
#!/usr/bin/env python3
from picamera2 import Picamera2
import time

picam2 = Picamera2()

# Full resolution, low frame rate to avoid microSD saturation
size = (4056, 3040)
config = picam2.create_video_configuration(
    raw={"format": 'SGBRG10', 'size': size},
    main={"size": (1920, 1080)},  # JPEG preview
    encode="main"
)
picam2.configure(config)

print("Starting 5-second raw video capture at 2 fps...")
print("(Expected write speed: ~36 MB/s, microSD max ~30 MB/s → may see frame drops)")

picam2.start()
for i in range(10):  # 10 frames × 2 fps = 5 seconds
    # Force synchronous capture (not background)
    picam2.capture_file("raw_frame_%04d.raw" % i)
    time.sleep(0.5)  # 2 fps

picam2.stop()
print("✓ Capture complete. Check for 'raw_frame_*.raw' files (18 MB each)")
```

Run it:
```bash
python3 capture_raw_video.py
```

**Expected behavior:**
- 10 raw frames saved (~180 MB total)
- Each frame is 10-bit SGBRG Bayer mosaic
- No JPEG generation (raw only = faster)

### 3.4 Metadata Capture (Exposure, Gain, Timestamp)

For BAM, metadata is critical (angle, laser power, exposure). Create `capture_with_metadata.py`:

```python
#!/usr/bin/env python3
from picamera2 import Picamera2
import libcamera
import json
import time

picam2 = Picamera2()
config = picam2.create_still_configuration(raw={})
picam2.configure(config)

picam2.start()
time.sleep(2)

# Capture with metadata
request = picam2.capture_request()

# Extract libcamera metadata
metadata = request.get_metadata()
exposure_us = metadata.get(libcamera.controls.ExposureTime, 0)
gain = metadata.get(libcamera.controls.AnalogueGain, 0)
awb_mode = metadata.get(libcamera.controls.AwbMode, 0)

# Create metadata JSON
meta = {
    "timestamp": time.time(),
    "exposure_us": exposure_us,
    "analog_gain": gain,
    "iso": int(gain * 100),  # Approximate ISO from gain
    "format": "SGBRG10",
    "resolution": [4056, 3040],
    "notes": "BAM baseline capture"
}

# Save both raw and metadata
request.save_dng("image.dng")
with open("image_meta.json", "w") as f:
    json.dump(meta, f, indent=2)

request.release()
picam2.stop()

print("✓ Metadata captured:")
print(json.dumps(meta, indent=2))
```

Run it:
```bash
python3 capture_with_metadata.py
```

---

## PART 4: REMOTE ACCESS FROM FEDORA KDE PLASMA

### 4.1 SSH Setup (Headless Control)

On Fedora laptop, find Pi's IP:
```bash
ssh pi@192.168.x.x
# (or use: ssh pi@raspberrypi.local if mDNS is configured)
```

First time: Accept key fingerprint, enter password.

### 4.2 X11 Forwarding (GUI Apps on Fedora Display)

From Fedora, run GUI apps on Pi, display on your Fedora desktop:

```bash
ssh -X pi@192.168.x.x
# Once connected:
libcamera-hello --timeout 5
# Preview appears on your Fedora screen!
```

**Note:** X11 forwarding has slight latency (~100-300ms), fine for setup, not for live streaming.

### 4.3 VNC for Better Remote Desktop (Optional)

For more responsive remote control:

```bash
# On Pi:
sudo apt install -y tightvncserver
vncserver :1 -geometry 1280x800 -depth 24

# On Fedora, install VNC viewer:
sudo dnf install -y tigervnc

# Connect:
vncviewer 192.168.x.x:1
```

---

## PART 5: STORAGE & FRAME RATE VALIDATION

### 5.1 Benchmark: How Many Frames Per Second?

The microSD write speed is your bottleneck. Test actual performance:

Create `benchmark_framerate.py`:

```python
#!/usr/bin/env python3
from picamera2 import Picamera2
import time
import os

picam2 = Picamera2()
size = (4056, 3040)
config = picam2.create_video_configuration(raw={"format": 'SGBRG10', 'size': size})
picam2.configure(config)

picam2.start()

# Capture 20 frames and measure time
start = time.time()
for i in range(20):
    picam2.capture_file("bench_%04d.raw" % i)

elapsed = time.time() - start
fps = 20 / elapsed

print(f"\n=== MicroSD Performance ===")
print(f"Frames captured: 20")
print(f"Time elapsed: {elapsed:.2f} seconds")
print(f"Actual framerate: {fps:.2f} fps")
print(f"Data rate: {fps * 18:.1f} MB/s")

picam2.stop()

# Cleanup
for i in range(20):
    os.remove("bench_%04d.raw" % i)
```

Run it:
```bash
python3 benchmark_framerate.py
```

**Expected results:**
- **MicroSD typical:** 1-2 fps (microSD ~20-30 MB/s sustained write)
- **Data rate:** ~18-36 MB/s (18 MB/frame × fps)

**If below 1 fps:** Your microSD may be defective. Upgrade to Kingston Canvas React or Samsung Evo Plus.

### 5.2 Calculate Storage for 5-10 Min Session

| Duration | Frame Rate | Total Frames | Size | Notes |
|----------|-----------|--------------|------|-------|
| **5 min** | 1 fps | 300 | 5.4 GB | Comfortable on 32GB microSD |
| **5 min** | 2 fps | 600 | 10.8 GB | Fills 32GB partially |
| **10 min** | 1 fps | 600 | 10.8 GB | Half of 32GB |
| **10 min** | 2 fps | 1200 | 21.6 GB | ~70% of 32GB |

**Phase 1 Recommendation:** Start with **1 fps for 10 minutes** → 10.8 GB (plenty of room for OS + scratch).

---

## PART 6: TROUBLESHOOTING

### Issue: "No camera detected"

**Cause:** CSI ribbon not properly seated or wrong port.

**Fix:**
1. Power off Pi completely
2. Remove microSD and wait 10 seconds
3. Reinsert microSD
4. Check CSI ribbon: contacts **face HDMI port**, ribbon is straight and fully seated
5. Reboot and try `libcamera-hello` again

### Issue: "Camera times out" / Blank preview

**Cause:** Camera not enabled in raspi-config or GPU memory too low.

**Fix:**
```bash
sudo raspi-config
# Enable Camera, set GPU Memory to 256MB
sudo reboot
```

### Issue: Frame drops or "only 5 frames captured instead of 10"

**Cause:** MicroSD write speed insufficient or thermal throttling.

**Fix:**
1. Run `benchmark_framerate.py` to verify actual fps
2. Reduce frame rate (try 1 fps instead of 2 fps)
3. Add heatsink to Pi CPU
4. Check `/opt/vc/bin/vcgencmd measure_temp` (should be <80°C)

### Issue: X11 forwarding doesn't work

**Cause:** X11 not enabled in SSH config.

**Fix (Fedora laptop):**
```bash
# Check if X11 forwarding is allowed:
grep "X11Forwarding" /etc/ssh/ssh_config

# If not present or "no", edit:
sudo nano /etc/ssh/ssh_config
# Add/uncomment: X11Forwarding yes

# Restart SSH:
sudo systemctl restart sshd
```

---

## PART 7: NEXT STEPS (PHASE 2)

Once you've verified raw capture is working:

1. **Order 500GB USB 3.0 SSD** (~₹3000-4000 / $40-50)
   - Will give 10x faster write speed (~150-250 MB/s)
   - Enables 5-10 fps sustained capture

2. **Set up SSD for auto-mount:**
   ```bash
   # Partition and format SSD as ext4
   # Add to /etc/fstab for automatic mounting
   ```

3. **Integrate with gonimeter motor control** (GPIO/I2C)

4. **Build Windows client** on your final Windows PC for remote BAM operation

5. **Field trial deployment** in your lab with technician

---

## SUMMARY: Phase 1 Completion Checklist

- [ ] **MicroSD card:** Flashed with Raspberry Pi OS Bookworm 64-bit
- [ ] **Hardware:** HQ Camera connected (CSI ribbon, contacts toward HDMI)
- [ ] **Software:** raspi-config camera enabled, GPU memory set to 256MB
- [ ] **Picamera2:** Installed and verified (`python3 -c "from picamera2 import Picamera2"`)
- [ ] **Raw capture:** Single DNG test working (`capture_raw_test.py`)
- [ ] **Video capture:** 20-frame raw video test working
- [ ] **Metadata:** JSON logging of exposure/gain working
- [ ] **Remote access:** SSH from Fedora laptop working
- [ ] **Frame rate:** Benchmark showing ~1-2 fps on microSD
- [ ] **Troubleshooting:** Know how to reseat CSI ribbon if needed

**You are now ready for Phase 2 (SSD + gonimeter integration).**

---

## APPENDIX: Command Reference

### Quick Camera Tests
```bash
# Live preview (5 seconds)
libcamera-hello

# Capture single JPEG
libcamera-jpeg -o test.jpg

# List available cameras
libcamera-hello --list-cameras

# Test with specific sensor mode
libcamera-hello --sensor-mode 2
```

### Picamera2 Python Quick Start
```python
from picamera2 import Picamera2

picam2 = Picamera2()
config = picam2.create_still_configuration()
picam2.configure(config)
picam2.start()
picam2.capture_file("image.jpg")  # JPEG
picam2.stop()
```

### System Monitoring
```bash
# CPU temperature
vcgencmd measure_temp

# RAM usage
free -h

# Disk usage
df -h

# Top processes
top

# Camera info
libcamera-hello --info-text "%rg %bg %focus"
```

---

**Document Version:** 1.0  
**Last Updated:** January 21, 2026  
**Status:** Phase 1 Ready
