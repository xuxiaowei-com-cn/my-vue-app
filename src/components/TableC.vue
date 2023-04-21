<script lang="ts">
import { h, defineComponent } from "vue";
import { ElTable, ElTableColumn, ElButton } from "element-plus";

export interface DataType{
    date:string
    name: string,
    state: string,
    city: string,
    address: string,
    zip: string,
}
interface Scope {
  row: Record<string, DataType>;
  $index: number;
}
export default defineComponent({
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    deleteRow: {
      type: Function,
      default: () => {},
    },
  },
  setup(props) {
    return () =>
      h(ElTable, { data: props.data, style: { width: "100%" }, maxHeight: 250 }, [
        h(ElTableColumn, { fixed: true, prop: "date", label: "Date", width: 150 }),
        h(ElTableColumn, { prop: "name", label: "Name", width: 120 }),
        h(ElTableColumn, { prop: "state", label: "State", width: 120 }),
        h(ElTableColumn, { prop: "city", label: "City", width: 120 }),
        h(ElTableColumn, { prop: "address", label: "Address", width: 600 }),
        h(ElTableColumn, { prop: "zip", label: "Zip", width: 120 }),
        h(
          ElTableColumn,
          { fixed: "right", label: "Operations", width: 120 },
          {
            default: (scope: Scope) => {
              return h(
                ElButton,
                {
                  link: true,
                  type: "primary",
                  size: "small",
                  onClick: () => props.deleteRow(scope.$index),
                },
                "Remove"
              );
            },
          }
        ),
      ]);
  },
});
</script>
