PS C:\Users\luo> adb shell "dumpsys SurfaceFlinger | grep DEV"
Display 4627039422300187648 (HWC display 0): port=0 pnpId=MTK displayName="MTKDEV"
           6 |            0 |     DEVICE |          0 |    0    0 3840 2160 |    0.0    0.0 3840.0 2160.0 |  60.00 ExactOrMultiple      OnlySeamless    [*]
           7 |            1 |     DEVICE |          0 |    0    0 3840 2160 |    0.0    0.0 3840.0 2160.0 |        Cat::NoPreference           Default    [*]
           8 |         2038 |     DEVICE |          0 | 1876   80 1964  168 |    0.0    0.0   88.0   88.0 |        Cat::NoPreference           Default    [ ]
           9 |         2038 |     DEVICE |          0 | 3162 1719 3303 1860 |    0.0    0.0  141.0  141.0 |        Cat::NoPreference           Default    [ ]
    deviceProductInfo={name="MTKDEV", manufacturerPnpId=MTK, productId=35638, manufactureWeek=42, manufactureYear=2021, relativeAddress=[]}
    name="MTKDEV"
Display 4627039422300187648 (physical, "MTKDEV")
      hwc: layer=0x08c4 composition=DEVICE (2)
      hwc: layer=0x08c1 composition=DEVICE (2)
      hwc: layer=0x0839 composition=DEVICE (2)
      hwc: layer=0x08c3 composition=DEVICE (2)
|      196 /      0 | 0xb4000077939d13f0 /     1635 | 7f000030 |   NON | DEV(      MM,DEV, HWCL:  461)   0|  0|  298188800 |0|0,  0,0,0,0,0, a, 2|         900|        a8000c02|      51|          0|         0|0,0, 1.00, 1.00|
|      193 /      1 | 0xb4000077939ccdd0 /     1591 |        1 |   PRE | DEV(      UI,DEV, HWCL:  448)   0|  0|          0 |0|0,  0,0,0,0,0, 0, 0|         b00|        20000c01|       0|          0|         0|0,0, 1.00, 1.00|
|       57 /      2 | 0xb4000077939cd1f0 /      457 |        1 |   PRE | DEV(      UI,DEV, HWCL:  448)   0|  0|          0 |1|0,  0,0,0,0,0, 0, 0|         b00|        20000c01|    4000|        164|         0|0,0, 1.00, 1.00|
|      195 /      3 | 0xb4000077939cc010 /     1608 |        1 |   PRE | DEV(      UI,DEV, HWCL:  448)   0|  0|          0 |1|0,  0,0,0,0,0, 0, 0|         b00|        20000c01|    4000|        164|         0|0,0, 1.00, 1.00|
----------DRMDEV Color Matrix----------
PS C:\Users\luo>

注意播放器格式。
