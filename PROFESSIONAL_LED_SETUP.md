# Professional LED Setup Guide - Advanced Animations

## 🎨 Overview

This guide shows you how to set up LEDs for **professional keyboard animations** like:
- ✨ Wave effects (left-to-right, top-to-bottom)
- 🌊 Ripple effects
- 🌈 Rainbow spectrum animations
- 💫 Breathing effects
- 🎯 Per-key reactive lighting
- 🔄 Multiple animation modes

**Good news:** ZMK firmware already includes all these effects! You just need to wire LEDs in the correct order.

---

## 🎯 Key Concept: Chain Order = Animation Flow

**CRITICAL:** The order you connect LEDs determines how animations flow!

```
If you chain LEDs like this:
LED1 → LED2 → LED3 → LED4 → LED5

Animations will flow in that order:
Wave: LED1 lights, then LED2, then LED3, etc.
```

### Example - Left to Right Wave:

```
Chain Order:  1 → 2 → 3 → 4 → 5

Animation frames:
Frame 1:  ●○○○○  (LED1 on)
Frame 2:  ○●○○○  (LED2 on)
Frame 3:  ○○●○○  (LED3 on)
Frame 4:  ○○○●○  (LED4 on)
Frame 5:  ○○○○●  (LED5 on)

Result: Wave moving left to right! 🌊
```

---

## 🎹 Split Keyboard LED Strategies

### Strategy 1: Underglow - Mirror Pattern (Recommended)

**Best for:** Symmetrical wave effects, professional look

```
LEFT HALF:                    RIGHT HALF:
                              
    1 ← 2 ← 3 ← 4 ← 5             5 → 4 → 3 → 2 → 1
    ↓                             ↓
    6                             6
    ↓                             ↓
    7 → 8 → 9 → 10                10 ← 9 ← 8 ← 7

Chain: P0.06 → 1→2→3→4→5→6→7→8→9→10
```

**Effect:** Animations flow outward from center or mirror each other

**Physical Layout:**
```
Top edge:      ● ● ● ● ●     ● ● ● ● ●
               1 2 3 4 5     5 4 3 2 1
               
Left side:     ●                       ● Right side
               6                       6

Bottom edge:   ● ● ● ● ●     ● ● ● ● ●
               7 8 9 10      10 9 8 7
```

### Strategy 2: Per-Key - Row by Row

**Best for:** Wave effects across keyboard, typing animations

```
LEFT HALF (35 keys):

Row 1:  1→ 2→ 3→ 4→ 5→ 6→ 7
Row 2:  8→ 9→10→11→12→13→14
Row 3: 15→16→17→18→19→20→21
Row 4: 22→23→24→25→26→27→28
Row 5: 29→30→31→32→33→34→35

Physical layout:
┌───┬───┬───┬───┬───┬───┬───┐
│ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │ 7 │
├───┼───┼───┼───┼───┼───┼───┤
│ 8 │ 9 │10 │11 │12 │13 │14 │
├───┼───┼───┼───┼───┼───┼───┤
│15 │16 │17 │18 │19 │20 │21 │
└───┴───┴───┴───┴───┴───┴───┘
```

**Effect:** Horizontal wave, row-by-row animations

### Strategy 3: Per-Key - Vertical Columns

**Best for:** Vertical wave effects, "rain" animations

```
LEFT HALF (7 columns × 5 rows):

Col 1: 1→ 6→11→16→21
Col 2: 2→ 7→12→17→22
Col 3: 3→ 8→13→18→23
Col 4: 4→ 9→14→19→24
Col 5: 5→10→15→20→25

Chain order: 1→6→11→16→21→2→7→12→17→22→3→...
```

**Effect:** Vertical wave top-to-bottom

### Strategy 4: Spiral Pattern

**Best for:** Unique spiral animations, attention-grabbing

```
LEFT HALF - Spiral from outside to center:

    1 → 2 → 3 → 4 → 5
    ↓               ↓
   16               6
    ↓               ↓
   15  13→14       7
    ↓   ↑          ↓
   12←11←10← 9 ← 8

Physical positions arranged in spiral chain order
```

**Effect:** Animation spirals inward or outward

---

## 🔧 Complete Wiring Guide

### For Underglow (10-20 LEDs per half)

#### LEFT HALF - Mirror Pattern:

**Physical Placement:**
```
        Top Edge
    ● ● ● ● ●
   [1][2][3][4][5]
    
●  [Keyboard]
[10] [Switches]
    
    ● ● ● ● ●
   [9][8][7][6]
      Bottom Edge
```

**Wiring Connections:**

1. **Power Bus (Red wire):**
   ```
   nice!nano VCC → All LED VDD pins (star configuration)
   ```

2. **Ground Bus (Black wire):**
   ```
   nice!nano GND → All LED GND pins (star configuration)
   ```

3. **Data Chain (White/Green wire):**
   ```
   nice!nano P0.06 → LED1 DIN
   LED1 DOUT → LED2 DIN
   LED2 DOUT → LED3 DIN
   LED3 DOUT → LED4 DIN
   LED4 DOUT → LED5 DIN
   LED5 DOUT → LED6 DIN
   LED6 DOUT → LED7 DIN
   LED7 DOUT → LED8 DIN
   LED8 DOUT → LED9 DIN
   LED9 DOUT → LED10 DIN
   LED10 DOUT → (unused)
   ```

**Chain Sequence:** Follow your chosen pattern (1→2→3→4→5→6→7→8→9→10)

#### RIGHT HALF - Mirror Pattern:

**Physical Placement:**
```
        Top Edge
    ● ● ● ● ●
   [5][4][3][2][1]
    
             ●  
[Keyboard]  [10]
[Switches]
    
    ● ● ● ● ●
   [6][7][8][9]
      Bottom Edge
```

**Data Chain:**
```
nice!nano P0.06 → LED1 DIN → LED2 DIN → ... → LED10 DIN
(Same as left, but physically mirrored)
```

---

### For Per-Key Backlighting (70 LEDs total)

#### LEFT HALF - 35 Keys:

**Physical Key Layout:**
```
┌───┬───┬───┬───┬───┬───┬───┐
│ ` │ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │  ← Row 1
├───┼───┼───┼───┼───┼───┼───┤
│TAB│ Q │ W │ E │ R │ T │ [ │  ← Row 2
├───┼───┼───┼───┼───┼───┼───┤
│CAP│ A │ S │ D │ F │ G │ ' │  ← Row 3
├───┼───┼───┼───┼───┼───┼───┤
│SFT│ Z │ X │ C │ V │ B │ \ │  ← Row 4
├───┼───┼───┼───┼───┼───┼───┤
│CTL│ALT│GUI│LOW│SPC│ENT│BSP│  ← Row 5
└───┴───┴───┴───┴───┴───┴───┘
```

**LED Chain Order (Row-by-Row for Left-to-Right Wave):**
```
LED Numbers:
┌───┬───┬───┬───┬───┬───┬───┐
│ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │ 7 │
├───┼───┼───┼───┼───┼───┼───┤
│ 8 │ 9 │10 │11 │12 │13 │14 │
├───┼───┼───┼───┼───┼───┼───┤
│15 │16 │17 │18 │19 │20 │21 │
├───┼───┼───┼───┼───┼───┼───┤
│22 │23 │24 │25 │26 │27 │28 │
├───┼───┼───┼───┼───┼───┼───┤
│29 │30 │31 │32 │33 │34 │35 │
└───┴───┴───┴───┴───┴───┴───┘
```

**Wiring Strategy:**

1. **Power Distribution (Star Pattern):**
   ```
   Create VCC bus wire running under all keys
   Create GND bus wire running under all keys
   
   Each LED:
   - VDD → VCC bus
   - GND → GND bus
   ```

2. **Data Chain (Row by Row):**
   ```
   nice!nano P0.06 → LED1 DIN
   
   Row 1: LED1 DOUT → LED2 DIN → LED2 DOUT → LED3 DIN → ... → LED7 DOUT
   Row 2: LED7 DOUT → LED8 DIN → LED8 DOUT → ... → LED14 DOUT
   Row 3: LED14 DOUT → LED15 DIN → ... → LED21 DOUT
   Row 4: LED21 DOUT → LED22 DIN → ... → LED28 DOUT
   Row 5: LED28 DOUT → LED29 DIN → ... → LED35 DOUT (unused)
   ```

**Physical Wiring:**
```
Under keyboard view:

VCC BUS ═══════════════════════════════════════
    │    │    │    │    │    │    │
   VDD  VDD  VDD  VDD  VDD  VDD  VDD
   LED1 LED2 LED3 LED4 LED5 LED6 LED7  ← Row 1
    │    │    │    │    │    │    │
    └────┴────┴────┴────┴────┴────┴───────
         ↓
   Data chain: DIN→DOUT→DIN→DOUT→...
         ↓
   LED8 LED9 LED10...                   ← Row 2
         ↓
   (Continue for all rows)
         ↓
GND BUS ═══════════════════════════════════════
```

---

## 🎨 ZMK Built-In Animation Effects

Your firmware already has these professional effects:

### Available Effects:

| Effect Name | Description | Best Chain Order |
|------------|-------------|------------------|
| **Solid** | Static color | Any |
| **Breathe** | Slow fade in/out | Any |
| **Spectrum** | Rainbow cycle all LEDs same color | Any |
| **Swirl** | Rainbow flows through chain | Sequential |
| **Wave** | Color wave through chain | Sequential row/column |

### Effect Controls (Already in Your Keymap):

Hold **LOWER** layer + these keys:

| Key | Function | What It Does |
|-----|----------|--------------|
| **U** | RGB_TOG | Toggle LEDs on/off |
| **I** | RGB_EFF | Next effect (Solid→Breathe→Spectrum→Swirl) |
| **H** | RGB_EFR | Previous effect |
| **O** | RGB_HUI | Hue + (change color) |
| **J** | RGB_HUD | Hue - (change color) |
| **P** | RGB_SAI | Saturation + (more vivid) |
| **K** | RGB_SAD | Saturation - (more pastel) |
| **[** | RGB_BRI | Brightness + |
| **L** | RGB_BRD | Brightness - |

---

## ⚙️ Advanced: Effect Speed Configuration

### In Your `.conf` File:

Add these to control animation speed:

```conf
# Animation speed (lower = faster, higher = slower)
CONFIG_ZMK_RGB_UNDERGLOW_SPD_START=3     # Default speed: 3
CONFIG_ZMK_RGB_UNDERGLOW_SPD_MIN=1       # Fastest speed
CONFIG_ZMK_RGB_UNDERGLOW_SPD_MAX=5       # Slowest speed
```

### To Add Speed Controls to Keymap:

Edit `caldera.keymap` and add:

```c
#include <dt-bindings/zmk/rgb.h>

// In your lower layer bindings:
&rgb_ug RGB_SPI    // Speed increase
&rgb_ug RGB_SPD    // Speed decrease
```

---

## 🎬 Animation Examples

### Wave Effect Left-to-Right:

**Chain Order:** Row by row (1→2→3→4→5→6→7→8→...)

**Result:**
```
Frame 1:  ●○○○○○○  Wave starts left
Frame 2:  ○●○○○○○  
Frame 3:  ○○●○○○○  Moves right
Frame 4:  ○○○●○○○  
Frame 5:  ○○○○●○○  
Frame 6:  ○○○○○●○  
Frame 7:  ○○○○○○●  Reaches right edge
```

### Rainbow Spectrum (All LEDs):

**Chain Order:** Any

**Result:** All LEDs cycle through rainbow colors together

```
All LEDs:  RED → ORANGE → YELLOW → GREEN → BLUE → PURPLE → RED...
```

### Swirl Effect:

**Chain Order:** Sequential (1→2→3→4→5...)

**Result:** Rainbow colors flow through chain

```
Frame 1:  R O Y G B P
Frame 2:  P R O Y G B
Frame 3:  B P R O Y G
Frame 4:  G B P R O Y
(Colors chase through the chain)
```

### Breathing Effect:

**Chain Order:** Any

**Result:** All LEDs fade in and out together

```
Brightness:  ░░▒▒▓▓██▓▓▒▒░░ (slow pulse)
```

---

## 💡 Recommended LED Counts by Setup Type

### Underglow Only (Simple):

**LED Count:** 10-15 per half
**Pattern:** Mirror perimeter
**Effects Work Best:** Breathe, Spectrum, Solid
**Battery Life:** Excellent (30-40 hours @ 30%)
**Complexity:** Easy

```
Simple underglow example:
    ● ● ● ● ●
  ●         ●
  ●         ●
    ● ● ● ● ●
```

### Underglow + Accent Keys (Balanced):

**LED Count:** 15-20 per half
**Pattern:** Perimeter + thumb cluster + function row
**Effects Work Best:** All effects
**Battery Life:** Good (20-25 hours @ 30%)
**Complexity:** Moderate

```
Combined example:
    ●F1●F2●F3●F4●   ← Function keys
    
    ● ● ● ● ●       ← Perimeter
  ●         ●
  ●    ●●●  ●       ← Thumb cluster
    ● ● ● ● ●
```

### Full Per-Key (Professional):

**LED Count:** 35 per half (70 total)
**Pattern:** Row by row
**Effects Work Best:** Wave, Swirl (spectacular!)
**Battery Life:** Limited (8-15 hours @ 20%)
**Complexity:** Advanced

```
Every key has LED:
┌●┬●┬●┬●┬●┬●┬●┐
├●┼●┼●┼●┼●┼●┼●┤
├●┼●┼●┼●┼●┼●┼●┤
└●┴●┴●┴●┴●┴●┴●┘
```

---

## 🔌 Wiring Summary by Setup Type

### Underglow (10 LEDs/half):

**Per Half:**
- 1× Data wire (nice!nano P0.06 to LED1 DIN)
- 1× VCC bus wire (red, ~30cm)
- 1× GND bus wire (black, ~30cm)
- 10× Short wires (data chain between LEDs, ~5cm each)
- Total: ~13 connections per half

**Time:** 1-2 hours per half

### Per-Key (35 LEDs/half):

**Per Half:**
- 1× Data wire (nice!nano P0.06 to LED1 DIN)
- 1× VCC bus wire (red, ~1m)
- 1× GND bus wire (black, ~1m)
- 35× Short wires (data chain, ~3cm each)
- 70× Power taps (VCC/GND to each LED)
- Total: ~140 connections per half

**Time:** 4-6 hours per half

---

## 🎯 Recommended First Build

### Start Simple, Expand Later:

**Phase 1: Basic Underglow (Week 1)**
```
- 10 LEDs per half
- Mirror perimeter pattern
- Test all effects
- Learn the system
- Battery life: 30-40 hours
- Cost: ~$10
```

**Phase 2: Add Accent Keys (Week 2)**
```
- Add 5 more LEDs per half (thumb keys)
- Chain them after perimeter
- More interesting effects
- Battery life: 20-25 hours
- Cost: +$5
```

**Phase 3: Full Per-Key (Optional)**
```
- Add remaining 20 LEDs per half
- Complete per-key backlighting
- Professional effects
- Battery life: 10-15 hours
- Cost: +$20
```

---

## ⚡ Power Consumption Planning

### By Setup Type @ 30% Brightness:

| Setup | LEDs/Half | Current Draw | Battery Life (350mAh) |
|-------|-----------|--------------|----------------------|
| Minimal | 5 | ~40mA | 40+ hours |
| Underglow | 10 | ~75mA | 30-35 hours |
| Balanced | 15 | ~110mA | 20-25 hours |
| Extended | 20 | ~150mA | 15-20 hours |
| Per-Key | 35 | ~250mA | 8-12 hours |

**All calculations at 3.7V with mixed colors**

---

## 🛠️ Configuration Files

### Update Firmware:

**1. Set LED Count (`caldera_left.overlay`):**
```c
led_strip: ws2812@0 {
    ...
    chain-length = <10>;  // Change to your LED count per half
    ...
};
```

**2. Enable Features (`caldera_left.conf`):**
```conf
CONFIG_ZMK_RGB_UNDERGLOW=y
CONFIG_ZMK_RGB_UNDERGLOW_ON_START=y
CONFIG_ZMK_RGB_UNDERGLOW_EXT_POWER=y
CONFIG_WS2812_STRIP=y

# Optional: Set defaults
CONFIG_ZMK_RGB_UNDERGLOW_HUE_START=180    # Cyan
CONFIG_ZMK_RGB_UNDERGLOW_SAT_START=100    # Full saturation
CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=30     # 30% brightness
CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=1      # Start with breathe
CONFIG_ZMK_RGB_UNDERGLOW_SPD_START=3      # Medium speed
```

**3. Repeat for Right Half**

---

## ✅ Step-by-Step Installation

### For Underglow (Easiest):

**Day 1: Planning**
1. ☐ Decide on LED count (10-15 recommended)
2. ☐ Choose chain pattern (mirror recommended)
3. ☐ Mark physical positions on keyboard
4. ☐ Number positions in chain order

**Day 2: Physical Installation**
1. ☐ Place LEDs at marked positions
2. ☐ Secure with double-sided tape
3. ☐ Run VCC bus wire (red)
4. ☐ Run GND bus wire (black)
5. ☐ Solder power to each LED (VDD/GND)

**Day 3: Data Chain**
1. ☐ Connect nice!nano P0.06 to LED1 DIN
2. ☐ Connect LED1 DOUT to LED2 DIN
3. ☐ Continue chain in order
4. ☐ Add hot glue for strain relief
5. ☐ Test with multimeter (no shorts!)

**Day 4: Firmware & Testing**
1. ☐ Update `chain-length` in firmware
2. ☐ Build firmware
3. ☐ Flash to keyboard
4. ☐ Power on - LEDs should light!
5. ☐ Test all effects (LOWER + I)
6. ☐ Adjust brightness (LOWER + [/L)

---

## 🎨 Effect Showcase

### What Each Effect Looks Like:

**Solid (Mode 0):**
- All LEDs same static color
- Change color with HUI/HUD
- Perfect for monochrome look

**Breathe (Mode 1):**
- Slow fade in/out
- Very smooth
- Easy on eyes
- Great for working

**Spectrum (Mode 2):**
- Rainbow cycle
- All LEDs change color together
- Smooth color transitions

**Swirl (Mode 3):** ⭐ BEST FOR SHOWING OFF
- Rainbow flows through LED chain
- Different colors on each LED
- Creates "chase" effect
- **Requires sequential chain order for best effect**

---

## 🔍 Troubleshooting Animations

### Problem: Effects don't look smooth

**Solutions:**
- Increase LED count (more LEDs = smoother)
- Adjust animation speed (CONFIG_ZMK_RGB_UNDERGLOW_SPD_START)
- Check all LEDs in chain are working

### Problem: Wave goes wrong direction

**Solutions:**
- Reverse your chain order
- Re-number LEDs in opposite direction
- Or just enjoy the different direction!

### Problem: Some LEDs different color in Swirl

**This is normal!** Swirl effect makes each LED different color
- That's what creates the flowing rainbow effect
- If you want same color, use Spectrum mode instead

### Problem: Animations too fast/slow

**Solutions:**
```conf
# In .conf file:
CONFIG_ZMK_RGB_UNDERGLOW_SPD_START=5  # Slower (1-5 range)
```

---

## 🎓 Pro Tips

1. **Test Chain Order First**
   - Connect just 3 LEDs
   - Test effects
   - Verify order is correct
   - Then add remaining LEDs

2. **Label Everything**
   - Number each LED position
   - Mark chain order on paper
   - Photo document before closing case

3. **Start with Lower Brightness**
   - 20-30% is plenty bright
   - Saves battery
   - Easier on eyes
   - Can always increase later

4. **Use Solid Color for Daily Use**
   - Save Swirl for showing off
   - Solid/Breathe for working
   - Spectrum for parties 🎉

5. **Keep Data Wires Short**
   - <10cm between LEDs ideal
   - Longer = more noise risk
   - Twist with GND if >10cm

---

## 📋 Quick Reference

### Default Keybindings:
```
LOWER + U = Toggle on/off
LOWER + I = Next effect
LOWER + O = Next color
LOWER + [ = Brighter
LOWER + L = Dimmer
```

### Effect Order:
```
Press I repeatedly to cycle:
Solid → Breathe → Spectrum → Swirl → (back to Solid)
```

### Best Chain Orders:
```
Left-Right Wave:   Row by row (1→2→3...)
Spiral:            Spiral pattern from edge
Underglow:         Perimeter (mirror pattern)
Random/Sparkle:    Any order works
```

---

## 🎉 Summary

### For Professional Animations:

✅ **Use WS2812B LEDs** (individual or strip)
✅ **Chain order determines animation flow**
✅ **ZMK has all effects built-in** (no extra work!)
✅ **Start with 10-15 LEDs per half** (good balance)
✅ **Mirror pattern for underglow** (looks professional)
✅ **Row-by-row for per-key** (best wave effects)
✅ **Test effects before closing case**
✅ **Keep brightness at 20-40%** (battery life + looks good)

### You Get These Effects Automatically:
- Wave animations ✅
- Rainbow spectrum ✅
- Breathing ✅
- Color cycling ✅
- Variable brightness ✅
- Multiple modes ✅

**No special wiring needed - just connect LEDs in the right order!**

---

**Ready to create professional keyboard lighting? Start with 10 underglow LEDs and expand from there!** 🎨✨