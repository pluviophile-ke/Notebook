3D-TextMeshPro 与 UI-TextMeshPro不一样，前者没有画布（Canvas）后者自带画布

### **在程序中更改text内容**

#### 方法一：

1. 在场景中放入一个3D-TextMeshPro
2. 创建一个c#代码，并将其附加到某个对象上
3. 在代码中加入`public TextMeshPro textMeshPro;`
4. 将TextMeshPro对象拖入c#脚本组件处
5. 使用代码`textMeshPro.text = $"output：{变量1} {变量2}";`

#### 方法二：

1. 在场景中放入一个3D-TextMeshPro
2. 创建一个c#代码，并将其附加到某个对象上
3. 在代码中加入`public GameObject textMeshPro; `
4. 将TextMeshPro对象拖入c#脚本组件处
5. 使用代码`textMeshPro.GetComponent<TextMeshPro>().text = $"{phi:0.0}°";`



### **从预制体中生成到场景**

1. 首先有一个3D-TextMeshPro的预制体

2. 创建一个c#代码，并将其附加到某个对象上

3. 在代码中写：

   ```c#
   public GameObject PhiDegreePrefab;		// 预制体
   private GameObject PhiDegreeInstance;	// 实例
   ```


4. 将预制体拖入C#脚本

5. 使用代码将预制体实例化

   ```C#
   PhiDegreeInstance = Instantiate(PhiDegreePrefab, startPosition, Quaternion.identity);
   ```

6. 调整在场景中的位姿和缩放

   ```c#
   // 将 phi 数值放在x轴与穿刺向量夹角处
   // 先调整 rotation
   // 计算在自定义坐标轴下的旋转
   Quaternion phiLocalRotation = Quaternion.LookRotation(phiTextForward, phiTextUp);
   // 调整为世界旋转
   PhiDegreeInstance.transform.rotation = axisInstance.transform.rotation * phiLocalRotation;
   
   // 再调整 positon
   // 计算与相同长度x轴的中点坐标
   Vector3 phiLocalPosition = ((Vector3.right * punctureVecMagnitude) + start) / 2;
   // 调整中点坐标为世界坐标
   PhiDegreeInstance.transform.position = axisInstance.transform.TransformPoint(phiLocalPosition);
   
   // 可选：缩放（一定是相对于gameObject的缩放）
   PhiDegreeInstance.transform.localScale = Vector3.Scale(PhiDegreeInstance.transform.localScale, (transform.localScale * 500) * 2f);
   // 可选：设置为皮肤的子对象
   PhiDegreeInstance.transform.SetParent(skin.transform, true);
   ```

   