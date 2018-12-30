# BestCheckpointCopier

Tensorflow Exporter that copies the best checkpoints

## Usage
```
  best_exporter = BestCheckpointCopier(
    name='best', # directory within model directory to copy checkpoints to
    checkpoints_to_keep=10, # number of checkpoints to keep
    score_metric='Loss/total_loss', # eval_result metric to use to determine "best"
    compare_fn=lambda x,y: x.score < y.score, # comparison function used to determine "best" checkpoint
    sort_key_fn=lambda x: x.score, # key to sort on when discarding excess checkpoints
    sort_reverse=False) # sort order when discarding excess checkpoints

  final_exporter = tf.estimator.FinalExporter(
    name=final_exporter_name, serving_input_receiver_fn=predict_input_fn)

  exporters = (best_exporter, final_exporter)

  eval_specs.append(
    tf.estimator.EvalSpec(
      name=str(eval_spec_name),
      input_fn=eval_input_fn,
      steps=None,
      exporters=exporters))
```
