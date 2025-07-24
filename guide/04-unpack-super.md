# 🗂️ Unpacking `super.img`

Modern Android devices (Android 10 and above) use a **dynamic partition** system. That means `system`, `vendor`, `product`, `odm`, etc., are all packed inside a single `super.img`.

This guide shows how to **unpack and extract these partitions** for editing or porting.

---

## 🧩 What is a Super Partition?

A `super.img` holds several logical partitions:

- `system`
- `vendor`
- `product`
- `odm`
- `system_ext`
- etc.

To modify any of these, you need to extract them first.

---

## 🔧 If You Have `super.img.lz4`

Some devices (Samsung, Huawei) ship `super.img.lz4`. First, convert it:

```bash
lz4 -d super.img.lz4 super.img

You now have a usable super.img.


---

🛠 Convert super.img (sparse) to RAW

You must convert sparse .img to raw format before extracting.

✅ Use simg2img:

simg2img super.img super.raw

You’ll get super.raw, which can be opened with 7Zip or CRB Kitchen.


---

📦 Extract Partitions

Now open super.raw using:

7Zip ZS

CRB Kitchen

AIK (Advanced)


You’ll find:

vendor.img

system.img

product.img

odm.img

etc.


> 📁 Extract them and rename each file properly.




---

🔁 If You Only Have vendor.img

If you don’t have a full super.img, you can still extract a single .img:

simg2img vendor.img vendor.raw

Then open vendor.raw in 7Zip or CRB Kitchen.


---

📺 Video Reference

▶️ Watch on YouTube:
How to Unpack super.img


---

✅ Summary Table

Image Format	Action

.lz4	Convert to .img using LZ4
.img (sparse)	Convert to .raw using simg2img
.raw	Extract with CRB/7Zip/AIK



---

> ✅ You are now ready to edit or port system-level images inside the super partition.



---

---
