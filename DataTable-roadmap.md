DataTable Roadmap
=================

3.5.0
-----
* Model/ModelList + View _(done)_
* Render performance _(~2x improvement so far. Ongoing)_
* Row filtering*
* Scrolling DataTable* _(in gallery module with some bugs)_
* Cell formatters/renderers* _(done)_
* Polling data source* _(via DataSource, no work needed)_
* Add, remove, update rows* _(done - datatable-mutable adds `addRow`, `removeColumn` etc)_
* Sortable columns*
* Custom sorting for columns*
* Cell, row, column navigation API (e.g. dt.cell(2,2), dt.cellAbove(cell)) _(`getCell`, `getRow` in core - done?)_
* Progressive enhancement
* ARIA
* Pagination
* Show/hide columns
* Message tbody API
* Fixed column widths _(min-width done. Overflow left to implementer)_

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