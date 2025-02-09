MergeIterator::next // ordered output
IteratorWrapper::next // not loaded -> loaded
PeekableLayerIterRef::next // enable peeking
LayerIterRef::next // include ImageLayer and DeltaLayer
DeltaLayerIterator::next // batched/bufferd
DeltaLayerIterator::next_batch // (Key, Lsn, Value)
