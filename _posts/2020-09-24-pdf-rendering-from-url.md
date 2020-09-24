---
layout: post
title:  "How to render PDF in android from URL, Assests, File."
categories: Load PDF
tags:  Load PDF, Render PDF, PDF from URL, PDF from Assets.
author: Parth Darji
---

* content
{:toc}

This article i will introduce how to render PDF from url.
This is more convenient and easy method to render PDF in android from url without downloading file in local storage.

## Follow steps

To render pdf from url you need library, please add below dependency in your app level gradle file build.gradle(Module:app)

![](https://i.imgur.com/acqUaUO.png")

```java
	implementation 'com.github.barteksc:android-pdf-viewer:2.8.2'
```
Now add below code in your xml file

```java
	 <com.github.barteksc.pdfviewer.PDFView
            android:id="@+id/pdfView"
            android:layout_width="match_parent"
            android:layout_weight="1"
            android:layout_height="0dp"/>
```

Place below code in your activity inside onCreate
and replace myPdfUrl with your actual pdf url 

```java
	 new RetrievePDFStream().execute(myPdfUrl);
```

add below Async function in your activity outside onCreate 
```java
	 public class RetrievePDFStream extends AsyncTask<String, Void, InputStream> {

        ProgressDialog progressDialog;
        protected void onPreExecute()
        {
            progressDialog = new ProgressDialog(LoadPdfActivity.this);
            progressDialog.setTitle("Fetching attachment...");
            progressDialog.setMessage("Please wait...");
            progressDialog.setCanceledOnTouchOutside(false);
            progressDialog.show();
        }
        @Override
        protected InputStream doInBackground(String... strings) {
            InputStream inputStream = null;

            try {

                URL urlx = new URL(strings[0]);
                HttpURLConnection urlConnection = (HttpURLConnection) urlx.openConnection();
                if (urlConnection.getResponseCode() == 200) {
                    inputStream = new BufferedInputStream(urlConnection.getInputStream());

                }
            } catch (IOException e) {
                return null;
            }
            return inputStream;

        }

        @Override
        protected void onPostExecute(InputStream inputStream) {
            pdfView.fromStream(inputStream)
                    .enableSwipe(true) // allows to block changing pages using swipe
                    .swipeHorizontal(false)
                    .enableDoubletap(true)
                    .defaultPage(0)
                    .onError(new OnErrorListener() {
                        @Override
                        public void onError(Throwable t) {
                            Toast.makeText(LoadPdfActivity.this,"Something went wrong, please contact administrator.",Toast.LENGTH_LONG).show();
                        }
                    })
                    .onPageError(new OnPageErrorListener() {
                        @Override
                        public void onPageError(int page, Throwable t) {
                            Toast.makeText(LoadPdfActivity.this,"Something went wrong, please contact administrator.",Toast.LENGTH_LONG).show();
                        }
                    })
                    .enableAnnotationRendering(false) // render annotations (such as comments, colors or forms)
                    .password(null)
                    .scrollHandle(null)
                    .enableAntialiasing(true) // improve rendering a little bit on low-res screens
                    // spacing between pages in dp. To define spacing color, set view background
                    .spacing(0).load();
            progressDialog.dismiss();
        }
    }
```
Now run your app and see your PDF will load in your app


