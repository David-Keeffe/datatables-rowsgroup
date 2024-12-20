# datatables-rowsgroup
The Datatables feature plugin that groups rows (merge cells vertically) in according to specified columns. It's inspired by [fnFakeRowspan] (https://datatables.net/plug-ins/api/fnFakeRowspan) DataTables plugin.

This fork includes updates to allow the plugin to work with DataTables 2.x: it's not backwards compatible. The main change is in the event names.
# Requirements
Requires DataTables v2.0+ and approproate jQuery version.

# Examples

Look at example.html

To use DataTables RowsGroup plugin, include all required js:

```
<script src="http://code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="http://cdn.datatables.net/2.0.0/js/jquery.dataTables.js"></script>
<script src="dataTables.rowsGroup.js"></script>
```

and just add array of the columns for 'rowsGroup' DataTable option for which you want enable the rows grouping (order is important):

```
var table = $('#example').DataTable({
	columns: [
		{
			title: 'First group',
		},
		{
			name: 'second',
			title: 'Second group [order first]',
		},
		{
			title: 'Third group',
		},
		{
			title: 'Forth ungrouped',
		},
		{
			title: 'Fifth ungrouped',
		},
	],
	data: data,
	rowsGroup: [// Always the array (!) of the column-selectors in specified order to which rows groupping is applied
				// (column-selector could be any of specified in https://datatables.net/reference/type/column-selector)
		'second:name',
		0,
		2
	],
})
```

Also supports manual remerge cells (if you manually deleted showed row, you should execute the method):
```
var table = $('#example').DataTable({...})
table.rowsgroup.update();
```

Or you can just set it to be remerged on next redraw (you might stack several times it and then call ```draw()```), and the ```update()``` procedure will be called once:
```
var table = $('#example').DataTable({...})
table.rowsgroup.updateNextDraw();
...
table.rowsgroup.updateNextDraw();
...
while (...) {
	...
	table.rowsgroup.updateNextDraw();
	...
}
table.draw();
```

# License
MIT License
