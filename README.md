# PDF Reader Kotlin

### Introduction:

This project is created in the intention to understand PDF Reader and make it as
readily usable component to integrate it with any projects

----------------------------------------------------------------------------------------------------

### Installation:

Step 1: Add the below dependency to build.gradle(Module:app)

``` 
implementation 'com.github.barteksc:android-pdf-viewer:3.0.0-beta.5'
```

----------------------------------------------------------------------------------------------------

### Coding Part:

1. Using below code in MainActivity to choose the file from file storage.

```
val browseStorage = Intent(Intent.ACTION_GET_CONTENT)
browseStorage.setType("application/pdf")
browseStorage.addCategory(Intent.CATEGORY_OPENABLE)
startActivityForResult(Intent.createChooser(browseStorage, "Select pdf"), 0)
```

Insert override method onActivityResult, add the below code to open the selected file from storage.

```
 if (requestCode == 0 && resultCode == RESULT_OK && data != null)
        {
            val selectedPdf = data.data
            val intent = Intent(this@MainActivity, ViewActivity::class.java)
            intent.putExtra("FileUri", selectedPdf.toString())
            startActivity(intent)
        }
```   
2. To View PDF file in our application

```
 val pdfFile = Uri.parse(intent.getStringExtra("FileUri"))
        pdfView.fromUri(pdfFile)
            .password(null)
            .defaultPage(0)
            .enableSwipe(true)
            .swipeHorizontal(false)
            .enableDoubletap(true)
            .load()
```
