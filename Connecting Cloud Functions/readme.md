

# Integrating Cloud Functions with Firestore


### Set up Firestore

- Navigation **Firestore**
- Click **Create Database**
- Click **Native mode (recommended)**, and then click **Continue**
- Choose **Region** from lab
- For Secure rules, select **Test** rules

### Create and Save a Collection

1. **Click** `Start collection`.

2. **Fill in the details** as follows, then click **Save**:

   - **Collection ID**: `customers`
   - **Document ID**: **`Randomly Genarate`**

3. **Add Fields** to the collection:

   - **Field name**: `firstname`
     - **Field type**: `string`
     - **Field value**: `Lucas`

   - Click the **Add a Field (+)** button to add another field:

     - **Field name**: `lastname`
       - **Field type**: `string`
       - **Field value**: `Sherman`


4. **Click Save** to finalize the collection.

---
#

Open the **Cloud Shell** terminal window.

```
export REGION=
```

```bash
curl -LO https://github.com/shaquib01/cloudskillsboost.google/raw/master/Connecting%20Cloud%20Functions/lab.sh
sudo chmod +x lab.sh
./lab.sh
```

---

## Wait for command to execute. 

### Now Delete the old field and again create the same.

 **Field name**: `lastname`
 - **Field type**: `string`
 - **Field value**: `Sherman`


---

## 🎉 Congratulations !!!

---
