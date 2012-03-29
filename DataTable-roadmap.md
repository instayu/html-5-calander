DataTable Roadmap
=================

Ongoing
-------
* Render performance -- ~2x overall speed improvement from 3.4.1 at last measure, but still a lot to do

3.5.0
-----
* <del>Model/ModelList + View</del> _(done)_
* <del>Row filtering</del> _(via ModelList `filter` method)_
* <del>Scrolling DataTable</del> _(done)_
* <del>100% width scrollable table</del> _(done)_
* <del>Cell formatters/renderers</del> _(done)_
* <del>Polling data source</del> _(via DataSource, no work needed)_
* <del>Add, remove, update rows</del> _(done)_
* <del>Sortable columns</del> _(done)_
* <del>Custom sorting for columns</del> _(done)_
* <del>Cell, row, column navigation API (e.g. dt.cell(2,2), dt.cellAbove(cell))</del> _(done)_
* <del>Multi-column sort</del> _(done)_
* <del>ARIA</del> _(done)_
* <del>Message tbody API</del> _(done)_
* <del>Fixed column widths</del> _(non-absolute width done in `datatable-column-widths`. Absolute widths left to implementer)_

3.6.0
-----
* Progressive enhancement (didn't make 3.5.0)
* Pagination (didn't make 3.5.0)
* Show/hide columns (didn't make 3.5.0)
* Inline cell editing (text input only)
* Popup cell editing
* Keyboard navigation of cells and rows
* cellClick etc events - Based on mosen's work
* Data types with auto-default formatter/parsers/editors(?) ('currency', 'date', etc)
* Cell, row, column highlight
* Cell, row, column(?) selection
* Complex selection (ctrl+/alt+/meta+)
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

3.8.0
-----
* Infinite Scroll
* Drag reorder columns
* Drag resizable column widths
* Freeze columns

\* Feature noted to make sure they are preserved after architectural changes.