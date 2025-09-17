## PDF.js module install link

     <script src="https://mozilla.github.io/pdf.js/build/pdf.mjs" type="module"> 
     </script>   
   
   
## SVG for the loader


        <svg class="animate-spin h-10 w-10 text-slate-300" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"><circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle><path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path> </svg>
    
    

## DOM ELEMENTS



         const dom = {
            // File handling elements
            fileInput: document.getElementById('pdf-file'),         // Hidden file input element
            loader: document.getElementById('loader'),              // Loading spinner overlay
            initialMessage: document.getElementById('initial-message'), // Welcome message

            // UI control elements
            controlsContainer: document.getElementById('controls-container'), // Navigation/zoom controls
            pdfNameEl: document.getElementById('pdf-name'),         // PDF filename display
            pageNumInput: document.getElementById('page-num-input'), // Page number input field
            pageCountEl: document.getElementById('page-count'),     // Total pages display
            zoomLevelEl: document.getElementById('zoom-level'),     // Zoom percentage display
            
            // Layout elements
            viewerContainer: document.getElementById('viewer-container'), // PDF container
            mainViewer: document.getElementById('main-viewer'),     // Main scrollable area
            fileOpener: document.getElementById('file-opener'),     // Initial "Open" button
            fileInfo: document.getElementById('file-info'),         // File info after loading
            
            // Button elements
            prevPageBtn: document.getElementById('prev-page'),      // Previous page button
            nextPageBtn: document.getElementById('next-page'),      // Next page button
            zoomInBtn: document.getElementById('zoom-in'),          // Zoom in button
            zoomOutBtn: document.getElementById('zoom-out'),        // Zoom out button
            
            // Canvas elements
            canvas: document.getElementById('pdf-render'),          // Canvas for PDF rendering
            ctx: document.getElementById('pdf-render').getContext('2d'), // 2D rendering context
        };