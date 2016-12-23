# Android4.1
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.pankaj.adpter41.MainActivity">

    <TextView
        android:text="Descending"
        android:layout_width="169dp"
        android:layout_height="wrap_content"
        android:id="@+id/textView2"
        android:layout_alignParentEnd="true"
        android:layout_marginEnd="194dp" />

    <TextView
        android:text="Asecending"
        android:layout_width="102dp"
        android:layout_height="wrap_content"
        android:id="@+id/textView"
        android:layout_below="@+id/textView2"
        android:layout_alignParentEnd="true"
        android:layout_marginEnd="30dp" />
</RelativeLayout>
-----------------------------------------
package com.example.pankaj.adpter41;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import android.os.Bundle;
import android.support.v4.app.ListFragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;
import android.widget.Toast;


public class LstFragment extends ListFragment{
    static ArrayList<String> data_source;
    static ArrayAdapter<String> adapter;
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        ViewGroup rootView = (ViewGroup) inflater.inflate(R.layout.fragmentlayout, container, false);
        // Create an array of string to be data source of the ListFragment
        String[] datasource={"Juice","Pear","Lettuce","Cheese","Orange","Sandwich","Chicken"};
        data_source=new ArrayList<String>(Arrays.asList(datasource));
        // Create ArrayAdapter object to wrap the data source
        adapter=new ArrayAdapter<String>(getActivity(),R.layout.rowlayout,R.id.textView,data_source);
        // Bind adapter to the ListFragment
        setListAdapter(adapter);
        //  Retain the ListFragment instance across Activity re-creation
        setRetainInstance(true);
        return rootView;

    }
    public static void
    sortList(int order){
        Collections.sort(data_source, new Sorter(order));
        adapter.notifyDataSetChanged();

    }

    // handle Item click event
    public void onListItemClick(ListView l, View view, int position, long id){
        ViewGroup viewg=(ViewGroup)view;
        TextView tv=(TextView)viewg.findViewById(R.id.textView);
        Toast.makeText(getActivity(), tv.getText().toString(),Toast.LENGTH_LONG).show();
    }

    static class Sorter implements Comparator<Object>{
        int order=-1;
        Sorter(int order){
            this.order=order;
        }

        public int compare(Object ob1,Object ob2){
            if(ob1.toString().compareTo(ob2.toString())==0) return 0;
            else if(ob1.toString().compareTo(ob2.toString())<0)
                return order;
            else
                return(-1*order);
        }

    }

}
------------------
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    
</LinearLayout>
