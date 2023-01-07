

```
jqgrid



$(grid_selector).jqGrid({  
                //direction: "rtl",    
colModel: [  
                    {  
                        name: 'myac', index: '', width: 80, fixed: true, sortable: false, resize: false,  
                        //formatter:'actions',  
                        formatter: function (value, grid, rows, state) { return "<a href=\"#\" style=\"color:#f60\" onclick=\"Modify(" + rows.id + ")\">Edit</a>" }  
                    
                    }
```



```
blooean  isExit = isExitTable();

if(isExit){

String sql = update certificate_status set certificate_flag = 'Y' where tablename="entityBean.getTablename()"  and schema_name in( entityBean.getunk() ;
getJdbcTemplate().update(sql,new object[]{
    
});
}
else{
String sql =" insert into certificate_status values(?,?,?,?),nsert into certificate_status values(?,?,?,?),nsert into certificate_status values(?,?,?,?);
getJdbcTemplate().update(sql,new object[]{
    
});
}


public blooean isExitTable(){
blooean result =true;
String sql="select count(1) from certificate_status where tablename='entitiBean.getTablename()'";
int res = getJdbcTemplate().query(sql);
if(res==0){
return result=false;
}
return result;
}    
```



```
jqgrid 代码片段
SourceURL: http://trirand.com/blog/jqgrid/jqgrid.html#


jQuery("#rowed2").jqGrid({
url:'server.php?q=3',
datatype: "json",
colNames:['Actions','Inv No','Date', 'Client', 'Amount','Tax','Total','Notes'],
colModel:[
{name:'act',index:'act', width:75,sortable:false},
{name:'id',index:'id', width:55},
{name:'invdate',index:'invdate', width:90, editable:true},
{name:'name',index:'name', width:100,editable:true},
{name:'amount',index:'amount', width:80, align:"right",editable:true},
{name:'tax',index:'tax', width:80, align:"right",editable:true},
{name:'total',index:'total', width:80,align:"right",editable:true},
{name:'note',index:'note', width:150, sortable:false,editable:true}
],
rowNum:10,
rowList:[10,20,30],
pager: '#prowed2',
sortname: 'id',
viewrecords: true,
sortorder: "desc",
gridComplete: function(){
var ids = jQuery("#rowed2").jqGrid('getDataIDs');
for(var i=0;i < ids.length;i++){
var cl = ids[i];
be = "<input style='height:22px;width:20px;' type='button' value='E' onclick=\"jQuery('#rowed2').editRow('"+cl+"');\" />";
se = "<input style='height:22px;width:20px;' type='button' value='S' onclick=\"jQuery('#rowed2').saveRow('"+cl+"');\" />";
ce = "<input style='height:22px;width:20px;' type='button' value='C' onclick=\"jQuery('#rowed2').restoreRow('"+cl+"');\" />";
jQuery("#rowed2").jqGrid('setRowData',ids[i],{act:be+se+ce});
}
},
editurl: "server.php",
caption:"Custom edit "
});
jQuery("#rowed2").jqGrid('navGrid',"#prowed2",{edit:false,add:false,del:false});

```

