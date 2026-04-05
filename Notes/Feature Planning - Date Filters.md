---
aliases:
  - Feature Planning/Date Filters
original_path: Notes/Work/aiquery.io/Tasks/Filtering Optimization/Feature Planning - Date Filters.md
base: Work
organization: "[[aiquery.io]]"
path_area: Tasks
categories:
  - "[[Work]]"
  - "[[aiquery.io]]"
  - "[[Tasks]]"
---
Version: 4.0.0
Description: This version explains in detail the split date-time field handling edge case.

# Date Filters Feature Plan

## Overview
A system to handle date-based filtering that converts user-friendly date inputs into appropriate range queries, supporting both epoch timestamps and ISO 8601 string formats, ensuring precise minute-level boundaries.

### Edge Case
Some date fields are separated and displayed as two fields in the UI.
For example:
- Schdules List:
    <!-- Received as -->
    - Start Date: '2024-01-01T00:00:00.000Z'
    <!-- Displayed as -->
    - Start Date: '2024-01-01'
    - Start Time: '00:00'

## Key Requirements

### 1. Data Format Handling
- Support both storage formats: (Some fields are stored as epoch timestamps, some as ISO 8601 strings)
  ```typescript
  // Epoch timestamp fields
  timestamp: 1744331518368

  // ISO 8601 string fields
  initiatedOn: "2025-04-10T10:00:00.000Z"
  ```

### 2. Range Boundary Precision
- All ranges must align to precise boundaries:
  ```typescript
  // Example: User selects "4/10/2025 10:15 AM"

  // As start of range:
  startTime = "2025-04-10T10:15:00.000Z"  // Start of minute

  // As end of range:
  endTime = "2025-04-10T10:15:59.999Z"    // End of minute
  ```

### 3. Server Filter Mapping
Convert user-friendly filters to server-compatible operators:
```typescript
// "Between" Filter
{
  timestamp: {
    gte: startEpoch,
    lte: endEpoch
  }
}

// "From" Filter
{
  timestamp: {
    gte: startEpoch
  }
}
```

## Filter Types

### 1. Between Filter
```typescript
// User Input: "4/10/2025 10:15 AM - 4/10/2025 02:30 PM"

// For Epoch Fields
{
  field: "timestamp",
  filter: {
    gte: 1744332900000,  // 2025-04-10T10:15:00.000Z
    lte: 1744354199999   // 2025-04-10T14:30:59.999Z
  }
}

// For ISO String Fields
// REVIEW: Ensure that gte and lte work correctly with ISO 8601 strings in the backend
{
  field: "initiatedOn",
  filter: {
    gte: "2025-04-10T10:15:00.000Z",
    lte: "2025-04-10T14:30:59.999Z"
  }
}
```

### 2. From Filter
```typescript
// User Input: "4/10/2025 10:15 AM"

// For Epoch Fields
{
  field: "timestamp",
  filter: {
    gte: 1744332900000  // 2025-04-10T10:15:00.000Z
  }
}
```

### 3. On Date Filter
```typescript
// User Input: "4/10/2025"
// Converts to full day range

// For Epoch Fields
{
  field: "timestamp",
  filter: {
    gte: 1744300800000,  // 2025-04-10T00:00:00.000Z
    lte: 1744387199999   // 2025-04-10T23:59:59.999Z
  }
}
```

### 4. At Time Filter
<!-- ! Do Something -->

## Implementation Steps

### Phase 1: Date Handling Utilities
1. Create format detection and conversion utilities
   ```typescript
   interface DateUtils {
     isEpochField(fieldName: string): boolean;
     isISOStringField(fieldName: string): boolean;
     toEpoch(date: Date, boundary: 'start' | 'end'): number;
     toISOString(date: Date, boundary: 'start' | 'end'): string;
   }
   ```

2. Implement boundary calculation utilities
   ```typescript
   interface BoundaryUtils {
     getMinuteStart(date: Date): Date;
     getMinuteEnd(date: Date): Date;
     getDayStart(date: Date): Date;
     getDayEnd(date: Date): Date;
   }
   ```

### Phase 2: Component Foundation
3. Create base date picker component
   - Use appropriate date picker library
   - Handle both date-only and date-time selections
   - Add validation for ranges

4. Implement filter type selector
   - Between/From/On Date options
   - Dynamic UI based on selection

### Phase 3: Filter Logic Implementation
5. Create filter transformer
   ```typescript
   interface FilterTransformer {
     transformToServerFilter(
       fieldName: string,
       filterType: 'between' | 'from' | 'onDate',
       values: Date | [Date, Date]
     ): ServerFilter;
   }
   ```

6. Add validation and error handling
   - Range validation (start before end)
   - Invalid date handling
   - Field format compatibility

### Phase 4: Integration
7. Connect with existing filter system
   - Integrate with filter form
   - Handle filter updates
   - Support filter reset

8. Add filter serialization
   - Save/restore filter state
   - URL parameter handling

### Phase 5: Testing & Refinement
9. Comprehensive testing
   - Unit tests for all date utilities
   - Integration tests for filter transformations
   - Boundary case testing

10. UI/UX polish
    - Loading states
    - Error messages
    - Accessibility
    - Mobile responsiveness

## Testing Checkpoints
1. Verify minute boundary precision
2. Confirm correct format handling (epoch vs ISO)
3. Test server filter generation
4. Validate range calculations
5. Check timezone handling

# Split DateTime Field Handling

## Assumptions and Edge Cases
1. When filtering on time component:
   - We MUST use the date from the same server datetime field
   - We DON'T need to sync with currently visible date column filter
2. Columns visibility doesn't affect filtering
3. Date and time components can have different filter types (one-sided vs two-sided)

## Filter Combination Examples

### Scenario 1: Only Time Filter
```typescript
// Server Field: start_date = "2024-03-20T14:30:00.000Z"

// UI Filter on start_time: "Between 10:00 and 16:00"
{
  start_date: {
    gte: "2024-03-20T10:00:00.000Z",
    lte: "2024-03-20T16:00:59.999Z"
  }
}
```

### Scenario 2: Only Date Filter
```typescript
// Server Field: start_date = "2024-03-20T14:30:00.000Z"

// UI Filter on start_date: "From March 15, 2024"
{
  start_date: {
    gte: "2024-03-15T00:00:00.000Z"
  }
}
```

### Scenario 3: Both Date and Time Filters
```ts
// Server Field: start_date = "2024-03-20T14:30:00.000Z"

// UI Filters:
// start_date: "Between March 15, 2024 and March 20, 2024"
// start_time: "Between 10:00 and 16:00"

// Combined Server Filter:
{
  start_date: {
    gte: "2024-03-15T10:00:00.000Z",  // Combine start date with start time
    lte: "2024-03-20T16:00:59.999Z"   // Combine end date with end time
  }
}
```

### Scenario 4: Mixed Filter Types
```typescript
// Server Field: start_date = "2024-03-20T14:30:00.000Z"

// UI Filters:
// start_date: "From March 15, 2024" (one-sided)
// start_time: "Between 10:00 and 16:00" (two-sided)

// Combined Server Filter:
{
  start_date: {
    gte: "2024-03-15T10:00:00.000Z",  // From date + start time
    lte: null                          // No end date, use end time for each day
  }
}
```

## Implementation Details

### 1. Split Field Configuration
```typescript
interface SplitDateTimeConfig {
  serverField: string;
  components: {
    date: {
      uiField: string;
      currentFilter: DateFilter | null;
    };
    time: {
      uiField: string;
      currentFilter: TimeFilter | null;
    };
  };
}

// Example
const config: SplitDateTimeConfig = {
  serverField: 'start_date',
  components: {
    date: {
      uiField: 'start_date',
      currentFilter: {
        type: 'from',
        value: '2024-03-15'
      }
    },
    time: {
      uiField: 'start_time',
      currentFilter: {
        type: 'between',
        start: '10:00',
        end: '16:00'
      }
    }
  }
}
```

### 2. Filter Combination Logic
```typescript
interface FilterCombiner {
  combineFilters(config: SplitDateTimeConfig): ServerFilter {
    const { date, time } = config.components;

    // Handle different combinations of filter types
    if (date.currentFilter && time.currentFilter) {
      return this.combineDateAndTimeFilters(
        date.currentFilter,
        time.currentFilter
      );
    }

    // Handle date-only filter
    if (date.currentFilter) {
      return this.createDateOnlyFilter(date.currentFilter);
    }

    // Handle time-only filter
    if (time.currentFilter) {
      return this.createTimeOnlyFilter(
        time.currentFilter,
        this.getDateFromServerField(config.serverField)
      );
    }
  }
}
```

### 3. Filter Type Handling
```typescript
interface FilterTypeHandler {
  handleMixedFilters(
    dateFilter: DateFilter,
    timeFilter: TimeFilter
  ): ServerFilter {
    switch(dateFilter.type) {
      case 'from':
        return this.handleFromDateWithTimeRange(
          dateFilter.value,
          timeFilter
        );
      case 'between':
        return this.handleDateRangeWithTimeRange(
          dateFilter.start,
          dateFilter.end,
          timeFilter
        );
      // ... other cases
    }
  }
}
```

## Potential Issues and Edge Cases

1. Time Range Crossing Midnight
```typescript
// If time filter is "Between 22:00 and 03:00"
// Need special handling for crossing to next day

// For date filter "On 2024-03-20"
{
  start_date: {
    gte: "2024-03-20T22:00:00.000Z",
    lte: "2024-03-21T03:00:59.999Z"  // Note the date change
  }
}
```md

2. Timezone Considerations
```typescript
// Need to ensure all datetime combinations respect the timezone
// of the original server field
```

3. Invalid Combinations
```typescript
// Need validation for cases like:
// Date: "Until 2024-03-15"
// Time: "From 16:00"
// How to handle these conflicting ranges?
```

## Testing Matrix
1. Single Component Filters
   - Date only (from/between/until)
   - Time only (from/between/until)
2. Combined Filters
   - All combinations of date and time filter types
   - Boundary cases (midnight crossing)
   - Timezone edge cases
3. Filter Updates
   - Updating date with existing time filter
   - Updating time with existing date filter
4. Filter Clearing
   - Clear date keeping time
   - Clear time keeping date