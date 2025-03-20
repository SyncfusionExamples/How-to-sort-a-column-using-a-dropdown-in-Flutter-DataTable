# How to sort a column using a dropdown in Flutter DataTable (SfDataGrid)?

In this article, we will show you how to sort a column using a dropdown in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) with the necessary properties. To sort a column using a dropdown, manually define [SortColumnDetails](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SortColumnDetails-class.html) objects and add them to the [sortedColumns](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/sortedColumns.html) collection of [SfDataGrid.source](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource-class.html). When a column is selected from the dropdown, it is added to this collection, and the grid sorts the data accordingly. Before applying a new sort, the existing sorted columns are cleared to ensure only the selected column is sorted. To perform sorting at runtime, call the [sort()](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/sort.html) method after updating the sortedColumns collection. The dropdown allows users to choose from available columns (eg : id, name, designation, salary), triggering sorting dynamically.

```dart
void _sortDataGrid(String columnName) {
    employeeDataSource.sortedColumns.clear();
    employeeDataSource.sortedColumns.add(
      SortColumnDetails(
        name: columnName,
        sortDirection: DataGridSortDirection.ascending,
      ),
    );
    employeeDataSource.sort();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Syncfusion DataGrid Sorting')),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(8.0),
            child: Container(
              height: 40,
              width: 200,
              decoration: BoxDecoration(
                border: Border.all(color: Colors.grey),
                borderRadius: BorderRadius.circular(5),
              ),
              padding: EdgeInsets.symmetric(horizontal: 8),
              child: DropdownButtonHideUnderline(
                child: DropdownButton<String>(
                  value: selectedColumn,
                  hint: const Text("Select Column to Sort"),
                  isExpanded: true,
                  icon: Icon(Icons.arrow_drop_down),
                  style: TextStyle(fontSize: 14, color: Colors.black),
                  items:
                      ["id", "name", "designation", "salary"].map((
                        String column,
                      ) {
                        return DropdownMenuItem<String>(
                          value: column,
                          child: Text(column.toUpperCase()),
                        );
                      }).toList(),
                  onChanged: (String? newValue) {
                    if (newValue != null) {
                      setState(() {
                        selectedColumn = newValue;
                      });
                      _sortDataGrid(newValue);
                    }
                  },
                ),
              ),
            ),
          ),
          Expanded(
            child: SfDataGrid(
              source: employeeDataSource,
              columnWidthMode: ColumnWidthMode.fill,
              columns: <GridColumn>[
                GridColumn(
                  columnName: 'id',
                  label: Container(
                    padding: EdgeInsets.all(16.0),
                    alignment: Alignment.center,
                    child: Text('ID'),
                  ),
                ),
                GridColumn(
                  columnName: 'name',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Name'),
                  ),
                ),
                GridColumn(
                  columnName: 'designation',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Designation'),
                  ),
                ),
                GridColumn(
                  columnName: 'salary',
                  label: Container(
                    padding: EdgeInsets.all(8.0),
                    alignment: Alignment.center,
                    child: Text('Salary'),
                  ),
                ),
              ],
            ),
          ),
        ],
      ),
    );
  }
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-sort-a-column-using-a-dropdown-in-Flutter-DataTable).