modetest
===

Mode setting test tool for DRM/KMS drivers

## Description

`modetest` is a command-line utility used to test and verify the functionality of DRM (Direct Rendering Manager) and KMS (Kernel Mode Setting) drivers.

### Installation

- **Source Code**: [Mesa / drm · GitLab](https://gitlab.freedesktop.org/mesa/drm)
- **Downloads**: [Index of /libdrm (dri.freedesktop.org)](https://dri.freedesktop.org/libdrm/)

**Compilation:**

```shell
./configure --prefix=/opt/ --host=aarch64-linux-gnu
make && make install
```

### Syntax

```shell
modetest [OPTION]...
```

### Options

**Query Options:**
```shell
-c      List connectors.
-e      List encoders.
-f      List framebuffers.
-p      List CRTCs and planes.
```

**Test Options:**
```shell
-P <plane_id>@<crtc_id>:<w>x<h>[+<x>+<y>][*<scale>][@<format>]   Set a plane.
-s <connector_id>[,<connector_id>][@<crtc_id>]:<mode>[-<vrefresh>][@<format>]   Set a display mode.
-C      Test hardware cursor.
-v      Test vertical blanking page flips.
-w <obj_id>:<prop_name>:<value>   Set a property.
```

**Generic Options:**
```shell
-a      Enable atomic mode setting.
-d      Drop master privileges after mode setting.
-M <module>      Specify the driver module to use.
-D <device>      Specify the device node to use.
```

### Driver Modules (Example Values for `<module>`)

- `i915`: Intel Integrated Graphics
- `amdgpu`: AMD Radeon Graphics
- `radeon`: Legacy AMD Radeon Graphics
- `nouveau`: Open-source NVIDIA Graphics
- `vmwgfx`: VMware Graphics
- `omapdrm`: TI OMAP Graphics
- `exynos`: Samsung Exynos Graphics
- `msm`: Qualcomm MSM Graphics
- `rockchip`: Rockchip Graphics

### Examples

**Query device information:**

```shell
modetest
```

**Test display on a MIPI-DSI device using the Rockchip driver:**

```shell
modetest -M rockchip -s 211@108:1200x1920 -v
```

This command will typically display a sequence of color blocks or test patterns on the screen.

**Test with hardware cursor:**

```shell
modetest -M rockchip -s 211@108:1200x1920 -C
```
