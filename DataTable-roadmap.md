DataTable Roadmap
=================

3.5.0
-----
* Model/ModelList + View (done)
* Render performance (~2x improvement so far. Ongoing)
* Row filtering*
* Scrolling DataTable* (in gallery module with some bugs)
* Cell formatters/renderers* (done)
* Polling data source* (via DataSource, no work needed)
* Add, remove, update rows* (done - datatable-mutable adds `addRow`, `removeColumn` etc)
* Sortable columns*
* Custom sorting for columns*
* Cell, row, column navigation API (e.g. dt.cell(2,2), dt.cellAbove(cell)) (`getCell`, `getRow` in core - done?)
* Progressive enhancement
* ARIA
* Pagination
* Show/hide columns
* Message tbody API
* Fixed column widths (min-width done. Overflow left to implementer)

3.6.0
-----
* Inline cell editing (text input only)
* Popup cell editing
* Keyboard navigation
* cellClick etc events - Based on mosen's work
* Data types with auto-default formatter/parsers/editors(?) ('currency', 'date', etc)
* Cell, row, column highlight
* Cell, row, column(?) selection
* Complex selection (ctrl+/alt+/meta+)
* Multi-column sort
* Inline cell editing (alternate inputs - select, radio, ???)
* Popup row editing

3.7.0
-----
* Expandable rows (child rows map to current columns)
* Expandable rows (expanded area is not bound to table format)
* Drag Reorder rows
* tfoot API
* tfoot summary options
* Checkbox select column
* 100% width scrollable table

3.8.0
-----
* Infinite Scroll
* Drag reorder columns
* Drag resizable column widths
* Freeze columns

\* Feature noted to make sure they are preserved after architectural changes.