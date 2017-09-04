# whatsapp_collapsingtoolbar
This project is all about the collapsing toolbar which will  change the colour of the tool bar while collapsing with respect to the dominant colour in the image and  gives a better colour matching ui.

<p><strong>What are we going to develop?</strong><br />

The application which we are going to develop is an whats app like collapsing tool bar which  will change the colour based on the dominant  colour present in image so that it can give an awesome ui experience.</p>
                            
Android studio, basic knowledge of card view, nested scrollview, toolbar.</h4>
<p><strong>Getting started:</strong><strong><br />
</strong>Lets get started by  creating an Android application and follow the steps below.</p>
<p><strong>Step 1. Add the following dependencies.</strong></p>
<p>The following dependencies should be added to the gradle file of your app.</p>
<pre>compile 'com.android.support:cardview-v7:24.2.0'
compile 'com.android.support:design:24.2.0'
compile 'com.android.support:palette-v7:24.2.0'//</pre>
<p><em>this will help you to get the dominant color from the image</em></p>
<pre>compile 'com.squareup.picasso:picasso:2.5.2'//</pre>
<p><em>this will help you to load the image from the internet</em></p>
<p><strong>Step 2. Add the  internet permission to the manifest.</strong></p>
<p>This permission will help you  to access the internet to load the images.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;uses-permission android:name="android.permission.INTERNET"/&gt;</pre>
<p><strong>Step 2. Add the  following to your &#8220;style.xml&#8221;</strong></p>
<p>This will help you  for the dynamic text appearance while the collapsing of the toolbar.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;style name="expandedtoolbar" parent="@android:style/TextAppearance.Medium"&gt;
    &lt;item name="android:textSize"&gt;45sp&lt;/item&gt;
    &lt;item name="android:textColor"&gt;#ffffff&lt;/item&gt;
    &lt;item name="android:textStyle"&gt;bold&lt;/item&gt;
&lt;/style&gt;

&lt;style name="collapsedtoolbar" parent="@android:style/TextAppearance.Medium"&gt;
    &lt;item name="android:textSize"&gt;18sp&lt;/item&gt;
    &lt;item name="android:textColor"&gt;#ffffff&lt;/item&gt;
&lt;/style&gt;</pre>
<p><strong>Step 3.  Now  we can start to design the layout &#8220;activity_main.xml&#8221;.</strong></p>
<p>This xml files contains  card view, collapsingtoolbarlayout, appbarlayout, textview,  imageview and etc.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="xml"> 
&lt;android.support.design.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"&gt;
    &lt;android.support.design.widget.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="250dp"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"&gt;
        &lt;android.support.design.widget.CollapsingToolbarLayout
            android:id="@+id/collapsing_toolbar"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:contentScrim="?attr/colorPrimary"
            app:layout_scrollFlags="scroll|exitUntilCollapsed"&gt;
            &lt;ImageView
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:scaleType="centerCrop"
                android:fitsSystemWindows="true"
                android:id="@+id/image"
                app:layout_collapseMode="parallax" /&gt;
            &lt;android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:layout_collapseMode="pin" /&gt;
        &lt;/android.support.design.widget.CollapsingToolbarLayout&gt;
    &lt;/android.support.design.widget.AppBarLayout&gt;
    &lt;android.support.v4.widget.NestedScrollView
        android:id="@+id/scroll"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:clipToPadding="false"
        app:layout_behavior="@string/appbar_scrolling_view_behavior"&gt;
        &lt;FrameLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"&gt;
            &lt;android.support.v7.widget.CardView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="24dp"
                app:cardElevation="@dimen/spacing_medium"
                app:cardUseCompatPadding="true"&gt;
                &lt;LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:orientation="vertical"&gt;
                    &lt;TextView
                        android:id="@+id/title"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_marginLeft="@dimen/spacing_large"
                        android:layout_marginRight="@dimen/spacing_large"
                        android:layout_marginTop="@dimen/spacing_large"
                        android:textAppearance="@style/TextAppearance.AppCompat.Headline"/&gt;
                    &lt;TextView
                        android:id="@+id/description"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_margin="@dimen/spacing_large"
                        android:text="@string/loremipsum"
                android:textAppearance="@style/TextAppearance.AppCompat.Body1"/&gt;
                &lt;/LinearLayout&gt;
            &lt;/android.support.v7.widget.CardView&gt;
        &lt;/FrameLayout&gt;
    &lt;/android.support.v4.widget.NestedScrollView&gt;
&lt;/android.support.design.widget.CoordinatorLayout&gt;
</pre>
<p><strong>Step 4.  Now  you start coding with the &#8220;MainActivity.java&#8221;.</strong></p>
<p>Define the following label  globally so that it can be used across various functions in the class.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">private CollapsingToolbarLayout collapsingToolbarLayout = null;</pre>
<p>Add  below code inside<strong> oncreate</strong> function  of the class.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">collapsingToolbarLayout = (CollapsingToolbarLayout) findViewById(R.id.collapsing_toolbar);

collapsingToolbarLayout.setTitle("Ferrari");//setting the title for the tool bar

Picasso.with(this)
        .load("http://www.wonderslist.com/wp-content/uploads/2015/04/Ferrari-LaFerrari.jpg")
        .resize(300, 300).centerCrop()
        .into(mImageview);//loading the image to the imageview using picasso

ToolbarTextAppearance();//its a function to which will take care of the the dynamic text appearance

 Thread thread = new Thread(new Runnable() {

     @Override
     public void run() {
         try  {
           
            ToolbarColor();//this function will help to determine the dominant colour of the image and set that colour to the toolbar and status bar.

           
         } catch (Exception e) {
             e.printStackTrace();
         }
     }
 });

 thread.start();//since thetoolbarcolour function has network call it has to run with the thread.</pre>
<p>*if any doubt checkout comments</p>
<p><strong>Step 5. &#8220;ToolBarTextAppearance</strong><strong>&#8221; function.</strong></p>
<p>This function will help you with the text appearance while collapsing and expanding of toolbar.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">private void toolbarTextAppernce() {
    collapsingToolbarLayout.setCollapsedTitleTextAppearance(R.style.collapsedtoolbar);
    collapsingToolbarLayout.setExpandedTitleTextAppearance(R.style.expandedtoolbar);
}</pre>
<p><strong>Step 5. &#8220;ToolBarColor</strong><strong>&#8221; function.</strong></p>
<p>This function will fetch the dominant colour from the image loaded from the internet using palette and changes the colour of the tool bar and status bar.</p>
<pre class="EnlighterJSRAW" data-enlighter-language="java">private void ToolbarColor() {
   

    try {
        URL url = new URL("http://www.wonderslist.com/wp-content/uploads/2015/04/Ferrari-LaFerrari.jpg");
        HttpURLConnection connection = (HttpURLConnection)
        url.openConnection();
        connection.setDoInput(true);
        connection.connect();
        InputStream input = connection.getInputStream();

//the image url will be converted to stream so that itcan be converted to the bitmap

       final Bitmap bitmap = BitmapFactory.decodeStream(input);

//bitmap will be used by palette to determine the dominant color in an image as bitmap will give access to each pixel of the image

      Palette.from(bitmap).generate(new Palette.PaletteAsyncListener() {
            @Override
            public void onGenerated(Palette palette) {
                Palette.Swatch dominant = palette.getDominantSwatch();

            //this will be used to get the dominant colour from the image

        collapsingToolbarLayout.setStatusBarScrimColor(dominant.getRgb());
        collapsingToolbarLayout.setContentScrimColor(dominant.getRgb());

                //setting the dominant colour to the toolbar

if (Build.VERSION.SDK_INT &gt;= 21) {// used only in lolipop and above devices
                    Window window = getWindow();
window.addFlags(WindowManager.LayoutParams.FLAG_DRAWS_SYSTEM_BAR_BACKGROUNDS);
window.clearFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
window.setStatusBarColor(dominant.getRgb());
   //Setting the dominant color to the status bar

                
               
    } catch (Exception e) {
        // Log exception

    }

}
</pre>
                             
<p><strong>Conclusion:</strong></p>
<p>The final result will look like this.</p>

<img class="alignnone size-medium" src="http://d1y1cbtych728q.cloudfront.net/uploads/2016/10/14122108/J0SLrCaRpy.gif" alt="" width="290" height="486">

<img class="alignnone size-medium" src="http://d1y1cbtych728q.cloudfront.net/uploads/2016/10/14121951/FrjgqNsHOi.gif" alt="" width="287" height="486">
