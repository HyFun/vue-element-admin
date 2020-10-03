<template>
  <div class="app-container">
    <el-table :data="tableData">
      <el-table-column label="信息">
        <template slot-scope="scope">
          <div>
            {{ scope.row.name }} <span v-if="scope.row.isMaster===1">(主)</span>
          </div>
        </template>
      </el-table-column>

      <el-table-column label="内存消耗">
        <template slot-scope="scope">
          <div>
            {{ scope.row.progress }}
          </div>
        </template>
      </el-table-column>

      <el-table-column label="应用">
        <template slot-scope="scope">
          <div>
            <DragArea :role-list="scope.row.appRoleList" role-type="app" :node-id="scope.row.id" />
          </div>
        </template>
      </el-table-column>

      <el-table-column label="引擎">
        <template slot-scope="scope">
          <div>
            <DragArea :role-list="scope.row.engineRoleList" role-type="engine" :node-id="scope.row.id" />
          </div>
        </template>
      </el-table-column>

      <el-table-column label="CWOS">
        <template slot-scope="scope">
          <div>
            <DragArea :role-list="scope.row.cwosRoleList" role-type="cwos" :node-id="scope.row.id" />
          </div>
        </template>
      </el-table-column>

      <el-table-column label="中间件">
        <template slot-scope="scope">
          <div>
            <DragArea :role-list="scope.row.middlewareRoleList" role-type="middleware" :node-id="scope.row.id" />
          </div>
        </template>
      </el-table-column>

    </el-table>
  </div>
</template>
<script>
// 组件
import DragArea from './DragArea'

export default {
  components: {
    DragArea
  },
  data() {
    return {
      tableData: [
        {
          id: '300a678d-4483-4100-a109-cc6e94c48222',
          name: 'Node_pc_01',
          isMaster: 1,
          progress: '85%',
          appRoleList: [
            {
              name: 'app_role_01'
            },
            {
              name: 'app_role_02'
            },
            {
              name: 'app_role_03'
            }
          ],
          engineRoleList: [
            {
              name: 'engine_role_01'
            },
            {
              name: 'engine_role_02'
            },
            {
              name: 'engine_role_03'
            }
          ],
          cwosRoleList: [
            {
              name: 'cwos_role_01'
            },
            {
              name: 'cwos_role_02'
            },
            {
              name: 'cwos_role_03'
            }
          ],
          middlewareRoleList: [
            {
              name: 'middleware_role_01'
            },
            {
              name: 'middleware_role_02'
            },
            {
              name: 'middleware_role_03'
            }
          ]
        },
        {
          id: 'afc06b45-aa5e-41aa-b206-d5b50f44ec33',
          name: 'Node_pc_02',
          isMaster: 1,
          progress: '85%',
          appRoleList: [
            {
              name: 'app_role_04'
            },
            {
              name: 'app_role_05'
            },
            {
              name: 'app_role_06'
            }
          ],
          engineRoleList: [
            {
              name: 'engine_role_04'
            },
            {
              name: 'engine_role_05'
            },
            {
              name: 'engine_role_06'
            }
          ],
          cwosRoleList: [
            {
              name: 'cwos_role_04'
            },
            {
              name: 'cwos_role_05'
            },
            {
              name: 'cwos_role_06'
            }
          ],
          middlewareRoleList: [
            {
              name: 'middleware_role_04'
            },
            {
              name: 'middleware_role_05'
            },
            {
              name: 'middleware_role_06'
            }
          ]
        }
      ]
    }
  }
}
</script>
